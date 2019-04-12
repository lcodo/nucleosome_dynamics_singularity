# nucleosome_dynamics_singularity

`singularity pull shub://nucleosome-dynamics/nucleosome_dynamics_singularity`


`singularity exec --bind /galaxy_data/nuclDyn_data/tests/:/galaxy_data/nuclDyn_data/tests nucleosome_dynamics_singularity_latest.sif  /home/NucleosomeDynamics/runNuclDyn   readBAM --input /galaxy_data/nuclDyn_data/tests/sample-data/cellcycleG2_chrII.bam --output /galaxy_data/nuclDyn_data/tests/sample-data/dataset_readBAM545858_galaxy.RData --type paired `
===================================================
===> Nucleosome Dynamics (docker version) v0.1 <===
===================================================

===> Running readBAM <===

-- loading /galaxy_data/nuclDyn_data/tests/sample-data/cellcycleG2_chrII.bam

reading file /galaxy_data/nuclDyn_data/tests/sample-data/cellcycleG2_chrII.bam
processing flags
processing strand +
processing strand -
-- saving /galaxy_data/nuclDyn_data/tests/sample-data/dataset_readBAM545858_galaxy.RData
