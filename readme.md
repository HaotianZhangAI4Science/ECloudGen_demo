<div align=center>
<img src="./configs/figs/ecloudgen_legend_color_green.png" width="90%" height="90%" alt="TOC" align=center />
</div>


Comming Soon! 

ECloudGen
=======

<img src='./configs/figs/liglava.gif' width='30%'/> <img src='./configs/figs/pkt_lig.gif' width='30%'/> <img src='./configs/figs/ligink.gif' width='30%'/>

This figure represent: Electron Clouds; Protein-Ligand Interactions; Latent Diffusion Process

## Environment 

### Install via conda yaml file (cuda 12.1)

```python
conda env create -f ecloudgen_env.yml
conda activate ecloudgen 
```

### Install manually 

This environment has been successfully tested on CUDA==12.1

```
# recommend using numpy<2
mamba create -n ecloudgen pytorch==2.2.2 torchvision==0.17.2 torchaudio==2.2.2 pytorch-cuda=12.1 plyfile pyg rdkit biopython easydict jupyter ipykernel lmdb mamba -c pytorch -c nvidia -c pyg -c conda-forge

conda activate ecloudgen

# optional 
pip install pyg_lib torch_scatter torch_sparse torch_cluster torch_spline_conv -f https://data.pyg.org/whl/torch-2.2.0+cu121.html 

mamba install openbabel scikit-learn scipy omegaconf einops accelerate h5py wandb xtb ignite gpytorch altair -c conda-forge

pip install moleculekit
```

## Data 

### Protein-ligand pair dataset preparation. 

You can download the raw data as provided in [ResGen](https://github.com/HaotianZhangAI4Science/ResGen). You can also download the processed protein-ligand pair from the [this link](https://drive.google.com/drive/folders/1CzwxmTpjbrt83z_wBzcQncq84OVDPurM). 

Note: [index.pkl](https://github.com/HaotianZhangAI4Science/ResGen/tree/main/data/crossdocked_pocket10),  [split_by_name.pt](https://github.com/HaotianZhangAI4Science/ResGen/tree/main/data). are automatically downloaded with the SurfGen code.  index.pkl saves the information of each protein-ligand pair, while split_by_name.pt save the train-test split of the dataset.

```shell
tar -xzvf crossdocked_pocket10.tar.gz
# Then follow the ./dataset/readme.md for processing protein-ligand dataset from scratch. 
```

## Generation 

<div align=center>
<img src="./configs/figs/ECloudGen.png" width="90%" height="90%" alt="TOC" align=center />
</div>


```shell
# modify the data path and batch_size in the ./configs/eclouddiff.yml 
python generate_from_pdb.py --pdb_file pdb_file ./play_around/peptide_example/7ux5_protein.pdb --lig_file ./play_around/peptide_example/7ux5_peptide.sdf --outputs_dir results
```

## Training 

The training process is released as train.py, the following command is an example of how to train a model.

```shell
# prepare a demo data
python ./datasets/generate_pktlig_data.py
# modify the data path and batch_size in the ./configs/eclouddiff.yml 
python train_eclouddiff.py 
```









