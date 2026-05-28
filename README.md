# 🧬 WGCNA Docker Environment

A Dockerized environment for performing **Weighted Gene Co-expression Network Analysis (WGCNA)** in R. This container includes all necessary dependencies, a demo R Markdown pipeline, and support for custom datasets via volume mounts.

![WGCNA schema](https://raw.githubusercontent.com/NebulaKit/docker-WGCNA/main/wgcna_schema.png)

---

## 📦 Pull the Docker Image

```bash
docker pull rsubioinfogroup/wgcna:latest
```


## 🚀 Run the Container

Start an interactive R session:
```bash
docker run -it rsubioinfogroup/wgcna:latest
```

Start with volume mount (necessary for using your own data):
```bash
docker run -it -v /path/to/your/local/folder:/home/data rsubioinfogroup/wgcna:latest
```
Replace /path/to/your/local/folder with your actual local directory path.
On Windows, use a path like:
-v C:/Users/YourName/Documents/WGCNA_data:/home/data

## 📊 Run the WGCNA Analysis in R

Run the built-in demo analysis:
```r
rmarkdown::render("WGCNA.Rmd")
```

Run with your own dataset:

Make sure your input .csv is placed in the mounted /home/data/ folder, then:

```r
rmarkdown::render("WGCNA.Rmd",
  params = list(
    input_file = "/home/data/your_dataset.csv"
  ),
  output_file = "/home/data/WGCNA_output.html"
)
```
Important: When using your own data, the file must be a CSV where:

1. Samples are in rows, and molecular features (e.g., lipids, genes, etc.) are in columns

2. The first column must be named Group and contain sample labels or phenotypes (e.g., disease vs control, treatment group, etc.)


Customize additional parameters (optional):
```r
rmarkdown::render("WGCNA.Rmd",
  params = list(
    input_file = "/home/data/your_dataset.csv",
    threshold = 0.25,
    minClusterSize = 30,
    module_merge_height = 0.3
  ),
  output_file = "/home/data/custom_WGCNA_report.html"
)
```

## 🧠 Notes
Use volume mounts to load your own datasets and save outputs to your local drive.

All key WGCNA parameters (e.g., soft thresholding, module size, merge height) can be adjusted via the params argument in rmarkdown::render().

Output HTML reports and results tables are automatically generated.
