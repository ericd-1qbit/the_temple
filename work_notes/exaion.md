ssh -p 31122 admsrv@91.239.56.145 -i ~/.ssh/id_ed25519_1qbit

scp -p 31122 admsrv@91.239.56.145 -i ~/.ssh/id_ed25519_1qbit 


python tests/profiling/generate_synthetic_images_timing.py --num_gpu 1 --train_batch_size 128


docker run --gpus 0 --ipc=host --memory=20g -it -v `pwd`:/workspace quay.io/1qbit/diffusion-models:base-devel bash -c "python tests/profiling/generate_synthetic_images_timing.py --num_gpu 1 --train_batch_size 128"


python tests/profiling/generate_synthetic_images_timing.py --num_gpu 1 --train_batch_size 128