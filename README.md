# rlProtGen (rL protein generator)
Generation of BackBones conditioned on theozyme geometry

Owners: Yakov Kipnis and Ariel Ben-Sasson

Version 0: unsupervised RL for generation of protein backbone from a set of constrained rotamers constituting a theozyme geometry

Instructions to build the conda env:
1.  clone environment:
    on a linux system:  conda env create -f environment.yml
    on a non linux system: conda env create -f environmentMin.yml
2.  activate environment:
    conda activate rlProtGen
3.  stage environemnt kernel to use on a jupyter notebook:
    python -m ipykernel install --user --name rlPrtoGen --display-name=rlPrtoGen
4.  check your kernels:
    jupyter kernelspec list
5.  open the notebook, select the "rlProtGen" kernel and enjoy. (or not)
