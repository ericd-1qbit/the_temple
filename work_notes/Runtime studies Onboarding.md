Goal: 
Study runtime in dependence of number of GPUs and image/dataset size on GCP and Exaion.

Method: 
1.) Use main runscript and run the setup with all relevant combinations of:
	- num GPUs [1,2,4,8]
	- train batch size
	- image size, input_dim unet
	- CelebA, LSUN

2.) Inspect total runtime for all these scenarios. 
3.) Add to spreadsheet & share on Confluence.

Details:
- development branch: `timing_benchmarks_add_dataset_handling`
- shell script with relevant commands: `./221102_runtime_studies_gcp_exaion_platforms.sh`
	- two sets of commands - for GCP (plain python) and for Exaion (docker)
	- docker command mounts the local directory using `-v pwd:/workspace`
	- that local directory shoud point to a local version of the development branch
- 