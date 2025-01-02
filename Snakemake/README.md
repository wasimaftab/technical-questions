# Snakemake questions

## Question 1

List all wildcards in the below rule:
```python
rule process_sample:
    input: "data/{sample}.txt"
    output: "results/{sample}.processed.txt"
    shell: "process {input} > {output}"
```

## Question 2
A colleague created the following Snakefile to process multiple samples:

```python
rule process_samples:
    input:
        "data/{sample}.txt"
    output:
        "results/{sample}.processed.txt"
    shell:
        "process_tool {input} > {output}"

rule all:
    input:
        "results/sample1.processed.txt",
        "results/sample2.processed.txt"
```
When he/she ran the workflow with `snakemake --cores 1`, the following error was raised. 
```
WorkflowError:
Target rules may not contain wildcards. Please specify concrete files or a rule without wildcards at the command line, or have a rule without wildcards at the very top of your workflow (e.g. the typical "rule all" which just collects all results you want to generate in the end).
```
All the necessary input files exist and in the correct location, and the colleague expected the two files specified in the `all` rule's `input` directive to be created.

What is the issue and how would you fix the Snakefile? 


## Question 3
A colleague has written the following Snakefile. However, the workflow fails with an error when they try to run it. They ask for your help to debug the issue.
```python
rule process_data:
    input:
        "data/{sample}.tsv"
    output:
        "results/{sample}.processed.tsv"
    shell: """
        awk '{ print "{sample}:", $1, $2 }' {input} > {output}
    """
```
**Error message**
```bash
$ snakemake --cores 1 results/sample1.processed.tsv
RuleException in rule process_data in file /opt/repos/technical-questions/Snakefile, line 1:
ValueError: unexpected '{' in field name, when formatting the following:

        awk '{ print "{sample}:", $1, $2 }' {input} > {output}
```

What is wrong with the rule? Why is the rule failing and how can you fix it?

## Question 4
A colleague is building a Snakemake workflow to analyse a dataset where the number of input files depends on the results of a preprocessing step. Specifically, the preprocessing step generates an unknown number of split files (split_1.csv, split_2.csv, etc.) based on the input dataset, and these split files need to be processed independently.

The colleague wrote the following workflow but encounters a problem: Snakemake cannot resolve the dynamically generated split files because their names are unknown until the workflow runs. The colleague asks for your help to resolve the issue.

```python
rule generate_example_input:
    output:
        "input.csv"
    shell: "echo $(( (RANDOM % 10) + 1 )) > {output}"

rule split_data:
    input:
        "input.csv"
    output:
        directory("splits")
    shell: """
        num=$(cat {input})
        for i in $(seq 1 $num) ; do
            echo $i > splits/split_${i}.csv
        done
    """

rule process_data:
    input: "splits/split_{i}.csv"
    output: "splits/split_{i}.processed.csv"
    shell: "echo $(( $(cat {input}) + 1 )) > {output}"

rule all:
    input:
        expand("splits/split_{i}.processed.csv", i=[1, 2, 3])
    output:
        "results.txt"
    shell: """
        num=0
        for file in {input} ; do
            num=$(( $num + $(cat $file) ))
        done
        echo $num > {output}
    """
```

How would you change the workflow so that it can run, regardless of the `input.csv` value?


## Question 5

A colleague is running a Snakemake workflow on an HPC system with SLURM as the job scheduler. Currently, they are executing the workflow as a single monolithic job with the following command:

```bash
snakemake --cores 16 --snakefile workflow/Snakefile
```
However, the workflow contains rules with varying computational requirements—some requiring high memory or multiple cores, and others requiring minimal resources. The current approach is leading to inefficient resource usage and frequent job failures when rules exceed the available memory.

Propose an alternative solution to better manage the execution of this workflow on the SLURM cluster. How would you configure the workflow to ensure that each rule's resource requirements are met?


## Question 6
Point out as many issues as you can in the below rule.

```python
rule create_base_config:
    input:
        orig_configfile=rules.clone_basepipeline.output.configfile,
        container_path=rules.pull_container.output,
    output:
        'config-base.yaml'
    log:
        'create_base_config.log'
    run:
        shutil.copy(input.orig_configfile, output[0])
        with open(output[0], 'r') as f:
            config = yaml.safe_load(f)
            content = f.read()

        main_url = config['container']
        modified_content = content.replace(main_url, Path(input.container_path).resolve())

        with open('config-base.yaml', 'w') as f:
            f.write(modified_content)
```


## Question 7
A workflow needs to generate publication-ready plots for multiple datasets using R. The datasets are provided as CSV files, and the desired output is a PDF file for each dataset, showing a scatter plot of two specified columns.

The team initially implemented the plotting with this rule:

```python
rule generate_plots:
    input:
        "data/{sample}.csv"
    output:
        "plots/{sample}.pdf"
    shell:
        "Rscript -e 'data <- read.csv(\"{input}\"); pdf(\"{output}\"); plot(data$x, data$y, main = \"Scatter Plot\"); dev.off()'"
```
This works but is difficult to modify when additional plotting parameters or complex preprocessing steps are required. Furthermore, debugging errors in this setup has been a challenge.

Propose an improved solution for implementing this workflow while ensuring it remains flexible for future modifications.


## Question 8
A colleague is running a Snakemake workflow on a cluster using the latest version of Snakemake and the SLURM scheduler. They have successfully used the following command in the past to execute their workflow:

```bash
snakemake --jobs 10 --cluster "sbatch --time=01:00:00 --mem=4G"
```
However, when attempting to run the same command recently, they encounter the following error:

```less
snakemake: error: ambiguous option: --cluster could match --cluster-generic-submit-cmd, --cluster-generic-status-cmd, --cluster-generic-cancel-cmd, --cluster-generic-cancel-nargs, --cluster-generic-sidecar-cmd
```
The colleague is puzzled because nothing about the cluster setup or the workflow has changed, and they do not understand why the command no longer works.

- What are the possible reasons for this error?
- How would you troubleshoot and resolve the issue?
