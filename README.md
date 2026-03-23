# VeCos
🚀 "VeCoS: A High-Affinity Protein–Ligand Generative Model Guided by Contrastive Dynamics and Chemical Semantics"
<img src="./img/VeCos_01.png" >

### 📢 Announcement
The code will be uploaded immediately after the paper is officially released.

### 🧩 Environment

The environment configuration is the same as that of [tagmol](https://github.com/moleculeai/TAGMol).

### 📊 Datasets

To run the code download [data.zip](https://drive.google.com/drive/folders/1YELgByuohhMjKkHfqChHUxmjgQEwlla9?usp=drive_link) and extract it to the ```./data``` directory.
The original CrossDocked protein pocket files are also included in [crossdocked_v1.1_rmsd1.0_pocket10.zip](https://drive.google.com/drive/u/0/folders/1tBVDMckeuiTmWsuAdFjA__p8mzHorHmA).

### 📄 Pretrained Models

Download the [pretrained_models.zip](https://drive.google.com/drive/folders/1YELgByuohhMjKkHfqChHUxmjgQEwlla9?usp=drive_link) and place it in the ```./pretrained_models``` directory.

### 🛠️ Training

```bash
cd VeCos
```
To train VeCos:

```bash
python ./scripts/train_our.py
```

### ⚙️ Sampling

To sample molecules for the test set in CrossDocked2020:

```bash
python ./scripts/sample_flow_VP_guide_our.py --config ./configs/sampling_guide.yml --result_path ./results/ --start_index 0 --end_index 99  --device cuda:0
```

### ⚖️ Evaluating

```bash
python ./scripts/evaluate.py ./results
```
Our evaluated results are provided in  [VeCos_results.pt](https://drive.google.com/drive/folders/1YELgByuohhMjKkHfqChHUxmjgQEwlla9?usp=drive_link).

[//]: # (### 💊 Generating for a Given Pocket)

[//]: # ()
[//]: # (When generating molecules for a given protein pocket, you need to calculate the pocket’s volume and area first to predict the number of atoms. In this work we use [pyKVFinder]&#40;https://lbc-lnbio.github.io/pyKVFinder/index.html&#41; for these calculations but you may use any other tool you are familiar with. Follow the [documentation]&#40;https://lbc-lnbio.github.io/pyKVFinder/package/installation/index.html&#41; to install.)

[//]: # ()
[//]: # (It is strongly recommended to install pyKVFinder in a new environment since its dependencies conflict with those used in PAFlow.)

[//]: # ()
[//]: # (Assume the environment used for PAFlow is named ```paflow``` and pyKVFinder is installed in the environment ```pykvfinder```. Given the PDB file of the protein pocket 2Z3H and the SDF file of its reference ligand as example, the molecule generation process proceeds as follows:)

[//]: # ()
[//]: # (-   Convert the reference ligand SDF file to a PDB file:)

[//]: # ()
[//]: # (```bash)

[//]: # (python ./scripts/data_preparation/sdf_to_pdb.py --ligand_sdf_path ./example/2z3h_ligand.sdf)

[//]: # (```)

[//]: # ()
[//]: # (-   Calculate the pocket’s volume and surface area:)

[//]: # ()
[//]: # (```bash)

[//]: # (conda activate pykvfinder)

[//]: # (python ./scripts/data_preparation/calculate_volume_area.py --pocket_path ./example/2z3h_pocket10.pdb --ligand_path ./example/2z3h_ligand.pdb)

[//]: # (```)

[//]: # ()
[//]: # (Output:)

[//]: # ()
[//]: # (```bash)

[//]: # (Volume: 232.63)

[//]: # (Area: 229.08)

[//]: # (```)

[//]: # ()
[//]: # (-   Generate molecules for the pocket:)

[//]: # ()
[//]: # (```bash)

[//]: # (conda activate paflow)

[//]: # (python ./scripts/sample_for_pocket.py --pdb_path ./example/2z3h_pocket10.pdb --volume 232.63 --area 229.08 )

[//]: # (```)

### Ackowledgements
This codebase was build on top of [PAFlow](https://github.com/CMACH508/PAFlow).
