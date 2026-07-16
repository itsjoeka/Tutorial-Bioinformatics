# Weeks 1–5 Field Guide: Computational Foundations

Open this file at the start of each session and work top to bottom through that week's section. Each step is something to actually type and run, not just read.

**Starting point (already done):** `~/bioinformatics_workshop` exists with `data/raw/` (downloaded fastq files), `data/qc/` (FastQC output), `run_fastqc.sh`, and the `fastqc_env` conda environment.

**Environments used this module:**
| Weeks | Environment | Created in |
|---|---|---|
| 1–2 | none needed (system bash/git) | — |
| 3–4 | `bioinfo-py` | Week 3, Step 3.1 |
| 5 | `bioinfo-r` | Week 5, Step 5.1 |

---

## Week 1: Advanced Bash & Text Processing

### Step 1.1 — Recap and workspace check
```bash
cd ~/bioinformatics_workshop
ls data/raw/
mkdir -p practice
```

### Step 1.2 — Build a small practice file
Working with a tiny hand-written file first means you can predict the answer before the command gives it to you, which is the fastest way to catch a mistake.
```bash
cd practice

cat > toy.fasta << 'EOF'
>seq1 short_example
ATGCGATCGATCGTAGCTAGCTAGCATCG
>seq2 another_example
ATGGGGCCCCAAAATTTTGGGGCCCC
>seq3 gc_rich_example
GCGCGCGCGCGCATATATAT
EOF

cat toy.fasta
```

### Step 1.3 — `grep`: finding things
```bash
# Count sequences (one header line per sequence)
grep -c "^>" toy.fasta

# Show just the headers
grep "^>" toy.fasta

# Show a header and the line right after it (-A 1 = 1 line After the match)
grep -A 1 "^>seq2" toy.fasta

# Case-insensitive search
grep -i "gc_rich" toy.fasta
```

### Step 1.4 — `sed`: stream editing
```bash
# Print only line 2
sed -n '2p' toy.fasta

# Delete every header line, keep only sequence
sed '/^>/d' toy.fasta

# Replace every T with U (DNA to RNA)
sed 's/T/U/g' toy.fasta

# Same, but skip header lines this time — the ! means "NOT this pattern"
sed '/^>/!s/T/U/g' toy.fasta
```

### Step 1.5 — `awk`: field-based processing
`awk` reads a file record by record. `NR` is the current line number, `NF` the number of fields, `$1`/`$2` etc. are individual fields.

**Sequence length per record (handles multi-line FASTA correctly):**
```bash
awk '
/^>/ {
    if (seqlen) print name, seqlen
    name = substr($0, 2)
    seqlen = 0
    next
}
{ seqlen += length($0) }
END { print name, seqlen }
' toy.fasta
```

**Now the important correction from last session.** You counted fastq reads with `grep -c "^@"`. That mostly works, but it can misfire, because fastq quality lines are plain text too and can legitimately start with the `@` character. The version below can't be fooled, because it just counts total lines and divides by 4 (every fastq read is exactly 4 lines):
```bash
awk 'END {print NR/4}' data/raw/YOUR_FILE.fastq
```

**Average read length across a whole fastq file:**
```bash
awk 'NR%4==2 {sum+=length($0); count++} END {print sum/count}' data/raw/YOUR_FILE.fastq
```

**GC content (whole file, one clean number):**
```bash
awk '
!/^>/ {
    total += length($0)
    gc += gsub(/[GCgc]/, "", $0)
}
END { printf "GC content: %.2f%%\n", (gc/total)*100 }
' toy.fasta
```
`gsub()` deletes every match it finds and returns how many it deleted, which is what makes this one-liner work: length is tallied *before* the G/C characters get stripped out of that line.

### Step 1.6 — Pipes and redirection
```bash
# Combine grep and wc instead of writing two separate commands
grep "^>" toy.fasta | wc -l

# Shortest and longest read in a fastq file
awk 'NR%4==2 {print length($0)}' data/raw/YOUR_FILE.fastq | sort -n | head -1
awk 'NR%4==2 {print length($0)}' data/raw/YOUR_FILE.fastq | sort -n | tail -1

# Send output to a file instead of the screen
awk 'NR%4==2 {print length($0)}' data/raw/YOUR_FILE.fastq > read_lengths.txt
```

### Step 1.7 — Regex quick reference
| Pattern | Meaning |
|---|---|
| `^` | start of line |
| `$` | end of line |
| `.` | any single character |
| `*` | zero or more of the previous character |
| `[ATCG]` | any one of A, T, C, or G |
| `[^ATCG]` | any character that is *not* A, T, C, or G |

```bash
# Flag any read containing a non-standard base
awk 'NR%4==2 && $0 !~ /^[ACGTN]+$/ {print "Non-standard base on line", NR}' data/raw/YOUR_FILE.fastq | head
```

### Step 1.8 — This week's capstone: `fasta_stats.sh`
Reuses the `for` loop from your first session, now doing something more useful than calling one tool.
```bash
cd ~/bioinformatics_workshop
nano fasta_stats.sh
```
```bash
#!/bin/bash
# fasta_stats.sh — read count, average length, GC% for every fastq file

DATA_DIR="./data/raw"

for fq in "$DATA_DIR"/*.fastq; do
    filename=$(basename "$fq")
    reads=$(awk 'END{print NR/4}' "$fq")
    avg_len=$(awk 'NR%4==2 {sum+=length($0); n++} END {printf "%.1f", sum/n}' "$fq")
    gc_pct=$(awk 'NR%4==2 {total+=length($0); gc+=gsub(/[GCgc]/,"",$0)} END {printf "%.2f", (gc/total)*100}' "$fq")
    echo "$filename: $reads reads, avg length ${avg_len} bp, GC ${gc_pct}%"
done
```
```bash
chmod +x fasta_stats.sh
./fasta_stats.sh
```

### Week 1 checklist
- [ ] Wrote a `grep` pattern using an anchor
- [ ] Used `sed` to substitute text on non-header lines only
- [ ] Wrote an `awk` script using `NR`, `NF`, and a field variable
- [ ] Can explain why `NR%4` matters for fastq but not fasta
- [ ] `fasta_stats.sh` runs cleanly across all downloaded samples

---

## Week 2: Git & GitHub for Reproducible Science

### Step 2.1 — Why this matters (30 seconds, not a lecture)
- Mistakes become recoverable instead of catastrophic
- Two people (or future-you) can work on the same project without overwriting each other
- A public repo is something real to link in a CV

### Step 2.2 — Check and configure git
```bash
git --version
git config --global user.name "Her Name"
git config --global user.email "her_email@example.com"
git config --global init.defaultBranch main
```

### Step 2.3 — Initialize a repo around existing work
```bash
cd ~/bioinformatics_workshop
git init
git status
```

### Step 2.4 — Stage and commit
```bash
git add run_fastqc.sh fasta_stats.sh
git commit -m "Add FastQC automation and fasta stats scripts"
git log --oneline
```

### Step 2.5 — `.gitignore` for bioinformatics
Code and metadata belong in git. Raw sequencing data does not, it's too large and it isn't something you edit by hand.
```bash
cat > .gitignore << 'EOF'
data/raw/*.fastq
data/raw/*.fastq.gz
data/qc/*.html
data/qc/*.zip
.DS_Store
__pycache__/
*.pyc
EOF

git add .gitignore
git commit -m "Ignore raw data and system files"
```

### Step 2.6 — Write a real README
```bash
cat > README.md << 'EOF'
# Bioinformatics Workshop

Scripts for downloading, quality-checking, and summarizing bacterial sequencing data.

## Requirements
- conda
- `fastqc_env` (see setup below)

## Setup
    conda create -n fastqc_env python=3.10 -y
    conda activate fastqc_env
    conda install -c bioconda fastqc sra-tools -y

## Usage
    ./run_fastqc.sh      # runs FastQC on everything in data/raw/
    ./fasta_stats.sh      # prints read count, length, and GC% per file
EOF

git add README.md
git commit -m "Add README"
```

### Step 2.7 — Push to GitHub
On github.com: New repository → name it `bioinformatics-workshop` → do **not** initialize with a README (yours already exists locally).
```bash
git remote add origin https://github.com/YOUR_USERNAME/bioinformatics-workshop.git
git branch -M main
git push -u origin main
```
**Note:** GitHub no longer accepts your account password for this. It'll ask for a personal access token (Settings → Developer settings → Personal access tokens) or you'll need SSH keys set up. Sort this out together the first time, it only needs doing once per machine.

### Step 2.8 — Branching
```bash
git checkout -b add-length-filter
# make a small edit to fasta_stats.sh here
git add fasta_stats.sh
git commit -m "Add minimum length filter option"
git checkout main
git merge add-length-filter
git push
```

### Week 2 checklist
- [ ] Repo initialized, first commit made
- [ ] `.gitignore` correctly excludes raw data
- [ ] README explains what the repo does and how to run it
- [ ] Successfully pushed to GitHub
- [ ] Created a branch, committed on it, merged it back

---

## Week 3: Python for Bioinformatics I

### Step 3.1 — Environment setup
```bash
conda create -n bioinfo-py python=3.10 -y
conda activate bioinfo-py
conda install -c conda-forge biopython pandas numpy matplotlib -y
```

### Step 3.2 — Same loop, new language
```bash
for file in data/raw/*.fastq; do
    echo "$file"
done
```
```python
import glob

for file in glob.glob("data/raw/*.fastq"):
    print(file)
```

### Step 3.3 — Functions and file I/O
```python
def read_fasta_headers(filepath):
    headers = []
    with open(filepath) as f:
        for line in f:
            if line.startswith(">"):
                headers.append(line.strip())
    return headers

print(read_fasta_headers("practice/toy.fasta"))
```

### Step 3.4 — Write a FASTA parser from scratch
Before letting a library do it, build it once by hand so the mechanics aren't a mystery.
```python
def parse_fasta(filepath):
    sequences = {}
    name = None
    seq_parts = []
    with open(filepath) as f:
        for line in f:
            line = line.strip()
            if line.startswith(">"):
                if name:
                    sequences[name] = "".join(seq_parts)
                name = line[1:]
                seq_parts = []
            else:
                seq_parts.append(line)
        if name:
            sequences[name] = "".join(seq_parts)
    return sequences

seqs = parse_fasta("practice/toy.fasta")
for name, seq in seqs.items():
    print(name, len(seq))
```
This is the Python translation of Week 1's `awk` sequence-length script. Same job, different tool.

### Step 3.5 — Biopython `SeqIO`
```python
from Bio import SeqIO

for record in SeqIO.parse("practice/toy.fasta", "fasta"):
    print(record.id, len(record.seq))
```

### Step 3.6 — Sequence operations
```python
from Bio.Seq import Seq

seq = Seq("ATGGCCATTGTAATGGGCCGCTGAAAGGGTGCCCGATAG")
print("Reverse complement:", seq.reverse_complement())
print("Translation:", seq.translate())
```

### Step 3.7 — GC content, the current Biopython way
```python
from Bio.SeqUtils import gc_fraction

for record in SeqIO.parse("practice/toy.fasta", "fasta"):
    print(f"{record.id}: {gc_fraction(record.seq) * 100:.1f}% GC")
```
**Worth knowing:** older tutorials online use `from Bio.SeqUtils import GC`. That function was deprecated in Biopython 1.80 and removed entirely in 1.82, so on any current install it will fail with an ImportError. `gc_fraction()` is the replacement, and it returns a fraction between 0 and 1, not a 0–100 percentage, hence the `* 100` above.

### Step 3.8 — Capstone: Biopython on real data, cross-checked against Week 1
```python
from Bio import SeqIO
from Bio.SeqUtils import gc_fraction

lengths, gc_values = [], []

for record in SeqIO.parse("data/raw/YOUR_FILE.fastq", "fastq"):
    lengths.append(len(record.seq))
    gc_values.append(gc_fraction(record.seq))

print(f"Reads: {len(lengths)}")
print(f"Average length: {sum(lengths)/len(lengths):.1f} bp")
print(f"Average GC: {(sum(gc_values)/len(gc_values))*100:.2f}%")
```
Compare these three numbers against what `fasta_stats.sh` printed for the same file in Week 1. They should agree closely. If they don't, that mismatch is a genuinely good debugging exercise, not a problem to paper over.

### Week 3 checklist
- [ ] `bioinfo-py` environment created and working
- [ ] Wrote a FASTA parser without any library
- [ ] Used `SeqIO.parse` correctly on both fasta and fastq
- [ ] Knows to use `gc_fraction`, not `GC`
- [ ] Cross-checked Python output against Week 1's bash output

---

## Week 4: Python for Bioinformatics II

### Step 4.1 — Setup check
```bash
conda activate bioinfo-py
python -c "import pandas, numpy, matplotlib; print('ready')"
```

### Step 4.2 — pandas basics
```python
import pandas as pd

df = pd.DataFrame({
    "sample": ["SRR1", "SRR2", "SRR3"],
    "reads": [120000, 98000, 135000],
    "gc_percent": [50.2, 49.8, 51.1]
})
print(df)
print(df.describe())
```

### Step 4.3 — Turn real FastQC output into one clean table
FastQC's `summary.txt` (inside each `*_fastqc.zip`) has three tab-separated columns: PASS/WARN/FAIL, module name, filename.
```bash
cd data/qc
mkdir -p extracted
for zipfile in *_fastqc.zip; do
    unzip -o "$zipfile" "*/summary.txt" -d extracted/
done
cd ../..
```
```python
import pandas as pd
import glob

rows = [
    pd.read_csv(f, sep="\t", header=None, names=["status", "module", "filename"])
    for f in glob.glob("data/qc/extracted/*/summary.txt")
]
all_summaries = pd.concat(rows, ignore_index=True)

pivot = all_summaries.pivot(index="filename", columns="module", values="status")
print(pivot)
```

### Step 4.4 — Filtering
```python
failed = all_summaries[all_summaries["status"] == "FAIL"]
print(failed)
```

### Step 4.5 — A first plot
```python
import matplotlib.pyplot as plt

all_summaries["status"].value_counts().plot(kind="bar")
plt.title("QC Status Across All Samples and Modules")
plt.ylabel("Count")
plt.tight_layout()
plt.savefig("qc_summary_plot.png")
plt.show()
```

### Step 4.6 — This week's capstone
Save the pivot table to `qc_summary.csv`, save the plot as `qc_summary_plot.png`, then commit both to the git repo from Week 2.
```python
pivot.to_csv("qc_summary.csv")
```
```bash
git add qc_summary.csv qc_summary_plot.png
git commit -m "Add aggregated QC summary table and plot"
git push
```

### Week 4 checklist
- [ ] Can load a table into pandas and inspect it
- [ ] Successfully parsed real FastQC summary files into one table
- [ ] Filtered a dataframe by a condition
- [ ] Produced and saved a plot
- [ ] Committed the output to git

---

## Week 5: R & Bioconductor Primer

### Step 5.1 — Environment setup
```bash
conda create -n bioinfo-r -c conda-forge r-base r-essentials -y
conda activate bioinfo-r
R --version
```

### Step 5.2 — R basics
```r
reads <- c(120000, 98000, 135000)
mean(reads)

samples <- data.frame(
  sample = c("SRR1", "SRR2", "SRR3"),
  reads = c(120000, 98000, 135000),
  condition = c("control", "treatment", "treatment")
)
print(samples)
```

### Step 5.3 — `dplyr` piping
```r
library(dplyr)

samples %>%
  filter(condition == "treatment") %>%
  arrange(desc(reads))
```

### Step 5.4 — Installing Bioconductor packages
```r
install.packages("BiocManager")
BiocManager::install()

# Confirm it works with a small package
BiocManager::install("Biostrings")
library(Biostrings)
```

### Step 5.5 — `ggplot2` basics
```r
library(ggplot2)

ggplot(samples, aes(x = sample, y = reads, fill = condition)) +
  geom_col() +
  theme_minimal() +
  labs(title = "Reads per Sample")

ggsave("reads_per_sample.png")
```

### Step 5.6 — A first PCA
Using simulated counts here on purpose, so the mechanics are the focus. Week 11 does this for real with actual RNA-seq data.
```r
set.seed(42)
counts <- matrix(rpois(600, lambda = 50), nrow = 100, ncol = 6)
colnames(counts) <- paste0("sample", 1:6)
condition <- rep(c("control", "treatment"), each = 3)

pca <- prcomp(t(counts), scale. = TRUE)
pca_df <- data.frame(pca$x, condition = condition)

ggplot(pca_df, aes(x = PC1, y = PC2, color = condition)) +
  geom_point(size = 3) +
  theme_minimal() +
  labs(title = "PCA of Simulated Samples (toy data)")

ggsave("toy_pca.png")
```

### Week 5 checklist
- [ ] `bioinfo-r` environment created and working
- [ ] Comfortable with `data.frame` and `%>%` piping
- [ ] `BiocManager::install()` completed without errors
- [ ] Produced a `ggplot2` figure and saved it
- [ ] Understands this week's PCA used simulated data, and why

---

## Troubleshooting (all five weeks)

| Problem | Likely cause / fix |
|---|---|
| `command not found` for python/pip/R packages | Wrong (or no) conda environment active. Check with `conda info --envs`, then `conda activate <name>`. |
| `Permission denied` running a `.sh` script | Forgot `chmod +x script.sh`. |
| `git push` asks for a password and rejects it | GitHub needs a personal access token or SSH key, not your account password. |
| Biopython `ImportError: cannot import name 'GC'` | Old syntax. Use `from Bio.SeqUtils import gc_fraction` instead. |
| `awk` GC/length numbers look wrong | Check whether the file is fasta (multi-line records, use the header-triggered script) or fastq (fixed 4-line records, use `NR%4`). Mixing the two logics up is the most common mistake this module. |
| R can't find a package after `BiocManager::install()` | Confirm `bioinfo-r` is the active conda environment, not `bioinfo-py` or base. |
