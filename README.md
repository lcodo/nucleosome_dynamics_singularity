Nucleosome Dynamics - Singularity
===================
Nucleosome Dynamics Singularity image is a containerized implementation of 'Nucleosome Dynamics suite'.

#### Nucleosome Dynamics
Nucleosome Dynamics is a suite of R programs for **nucleosome-related analyses** based on MNase-seq experimental data. The toolkit includes the following analyses:

- nucleR: define and classify the location of nucleosomes from MNase-seq data.
- Nucleosome Dynamics: compares different MNase-seq experiments identifying variations in nucleosomes location.
- NFR: locate nucleosome-free regions
- Periodicity: predicts  nucleosome phasing at gene level
- TSS: classify transcription start sites based on the surrounding nucleosomes
- Stiffness: computes nucleosome stiffness derived from a Gaussian function fitting

#### Container software 
This singularity image extends and distributes the following rellevant software:

* R libraries:
   * NucleR R library: https://github.com/nucleosome-dynamics/nucleR
   * Nucleosome Dynamics R library: https://github.com/nucleosome-dynamics/NucDyn
* R programs:
   * Nucleosome Dynamics analyses: https://github.com/nucleosome-dynamics/nucleosome_dynamics

# Running Nucleosome Dynamics
Before using Singularity, you've to install singularity, if not previously done, you can do it by following the instructions from [Singularity install] (https://singularity.lbl.gov/docs-installation#install-the-master-branch) 

The Singularity image for Nucleosome Dynamics can be found at [singularity hub](https://singularity-hub.org/collections/2579) as `nucleosome-dynamics/nucleosome_dynamics_singularity`. The image can be pulled by following the next command.
```sh
singularity pull shub://nucleosome-dynamics/nucleosome_dynamics_singularity
```
### Running an individual analysis
You can run manually your containers using the following command:

```sh
singularity run --bind /path/to/data_dir/:/path/to/data_dir nucleosome_dynamics_singularity_latest.sif   [analysis] [analysis_options]
```

A short description of the parameters would be:
- `singularity run` will run the container for you.
- `--bind /path/to/data_dir/:/path/to/data_dir` will make the `data_dir` where input files are stored available to the container
- `nucleosome_dynamics_singularity_latest.sif` is the image name, which can be found at [singularity hub] (https://singularity-hub.org/collections/2579).
- `[analysis] [analysis_options]` correspond to the analysis type you want to run and its paremeters.

Available analysis are:

| `[analysis]` | Description |
| -------- | -------- |
| readBAM         | Read Aligned MSase-seq BAM into a RData structure (required for further process) |
| nucleR           | Determine the positions of the nucleosomes across the genome |
| NFR             | Short regions depleted of nucleosomes |
| txstart         | Classify Transciption start accordint to the properties of surrounding nucleosomes  |
| periodicity  | Periodic properties of nucleosomes inside gene bodies |
| stiffness | Aparent stiffness constant foreach nucleosome obtained by fitting the coverage to a gaussian distribution |
| nucleR_stats|  Nucleosome call statistics|
| nucDyn          | Comparison of two diferent MNase-seq experiments to nucleosome architecture local changes |
| NFR_stats|             Nucleosome Free Regions statistics|
| txstart_stats|         TSS and TTS statistics|
| periodicity_stats|  Statistics on Nucleosome periodicity|
| stiffness_stats|      Statistics on stiffness|
| nucDyn_stats|    Statistics on Nucleosome Dynamics analysis|


Each analysis has its own input files and arguments. `singularity run nucleosome_dynamics_singularity_latest.sif [analysis] --help` will display such information in detail. Yet, a full usage description can be found at the [Nucleosome Dynamics repository](https://github.com/nucleosome-dynamics/nucleosome_dynamics).

#### Example

Here is an example on how to load a MNase-seq reads file using `readBAM`. It takes as input a BAM file and convert it into an RData file ready to be feed to other analyses ('nucleR', 'NFR', etc.).

```sh
singularity run --bind $PWD/test/data/:$PWD/test/data nucleosome_dynamics_singularity_latest.sif readBAM --input $PWD/test/data/cellcycleG2_chrII.bam --output $PWD/test/data/cellcycleG2_chrII.RData --type paired
```

# Running a workflow script
You can combine different analysis tools to build your own workflow, you can do it following this command:

```sh

singularity run --bind /path/to/data_dir/:/path/to/data_dir nucleosome_dynamics_singularity_latest.sif  run  [WF_file_path]

```
Where:
- `WF_file_path`: is a bash file containing the Rscript calls to different analyses.

#### Example

Here is an example on how to run the test workflow file `test/scripts/wf-test.sh`, a bash file sequencially calling all 'Nucleosome Dynamics' analyses.

```
singularity run --bind $PWD/test/data:$PWD/test/data nucleosome_dynamics_singularity_latest.sif  run $PWD/test/scripts/wf-test.sh 
```
