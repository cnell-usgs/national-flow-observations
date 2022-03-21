# national-flow-observations
This repository pulls national flow data from NWIS for 50 states and all territories. The pipeline pushes to a shared cache in an S3 bucket called [ds-pipeline-national-flow-observations](https://s3.console.aws.amazon.com/s3/buckets/ds-pipeline-national-flow-observations/?region=us-west-2&tab=overview).

As of 2022, the repo is set-up for use on Tallgrass because Yeti will be removed from service in August 2022. The 2022 version of this repo is currently cloned here: `/caldera/projects/usgs/water/iidd/datasci/data-pulls/national-flow-observations`

## To run on Tallgrass with Singularity:
These are exact commands for Tallgrass.

After cloning the repo, pull the docker image from code.chs.usgs.gov:

```
module load singularity
singularity pull --docker-login docker://code.chs.usgs.gov:5001/wma/wp/national-data-pulls:v0.0
```
After you run the commands above you will see a prompt for a password. The password it is looking for is your [personal access token (PAT)](https://code.chs.usgs.gov/-/profile/personal_access_tokens). If you do not have a PAT set up you will need to do so.

Two Slurm scripts are included in this repo.  If you want to run Rstudio to do development work, run `sbatch launch_rstudio.slurm` and then follow the instructions in the Slurm output file (`shellLog/rstudio.out`) to make an SSH tunnel and log in to Rstudio via a browser.

To run the pipeline as a non-interactive batch job, open `run_scmake.slurm` and modify parameters like job length (`--time`) and partition (`-p`) as needed for how long you expect the job to run (see [this issue](https://github.com/USGS-R/national-flow-observations/issues/4) for estimates). Submit the job with `sbatch --mail-user=$USER@usgs.gov run_scmake.slurm`.
