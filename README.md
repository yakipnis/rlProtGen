# rlProtGen (rL protein generator)
Generation of BackBones conditioned on theozyme geometry

Owners: Yakov Kipnis and Ariel Ben-Sasson

Version 0: unsupervised RL for generation of protein backbone from a set of constrained rotamers constituting a theozyme geometry.

The goal here is to explore idea that protein backbones conditioned on external structural constraints represented by theozymes can be generated using trained RL agent from limited set of structural "letters". Letters are fragments of native protein backbones, representing recurrent structural motifs and stored as coordinates of CA atoms. There are two kinds of letters -- 4mer and 6mer.

4mers originate from continuous fragments of native protein backbones. Fragment length needs to be as small as possible to minimize structural diversity and allow clustering into finite number of distinct letters, while allowing unambiguous addition of letters by simple geometrical superposition of 3mer suffix and 3mer prefix of consequtive letters (using Kabsch algorithm).

It appears that regardless of precise choice of protocol used to generate alphabet of 4mers, any arbitrary protein scaffold can be "traced" in visually recognizable form by sequential addition of letters, which suggests that even protein topologies not currently observed can be generated (tapping into Dark Protein Universe). String of letters from structural alphabet provides compact and structurally unique encoding of protein topology as opposed to ABEGO string from Rosetta blueprint.

However, it is known that non-local features of protein topologies are hard to capture using only sequential mode of protein backbone extension by 4mers. Here we propose special kind of letters in attempt to mitigate this problem. Most non-local interactions in proteins are stabilized by either H-bonds or VdW-interactions (other interactions can be treated the same way if expansion of alphabet needed). 6mers are letters capturing common structural motifs containing such interactions. Two non consequtive residues i and j, forming backbone H-bonds or VdW contact, are extracted from native proteins along with four flanking residues i-2, i-1, j+1, j+2. Such discontinuos fragments are clustered to identify common motifs and can be used as letters. Intuition behind these type of letters is that their use may promote seeding and subsequent elongation by 4mers of properly spaced secondary structure elements.  **Their usefulness is yet to be established, though**.

Since in this project we are planning to use RL framework, three components of it -- environment, agent, action space -- need to be defined.
Environment is imagined as a GRID of irregularly spaced nodes. Fundamental properties of the GRID is that each node in the GRID cannot have neighbors closer than DMIN (clash), can have no more than 2 neighbors separated by 3.8A distance (DMIN<=dist<=DMAX), there are no nodes with no neighbors in DMIN<=dist<=DMAX (**singleton**) (Discuss source of singletones???)


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
