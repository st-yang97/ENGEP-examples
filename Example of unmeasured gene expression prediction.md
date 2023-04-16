# Prediction of unmeasured genes

This example use ENGEP to predict unmeasured genes for osmFISH.

Load ENGEP package.

```
library(ENGEP)
```

Read the spatial dataset. 

```
osmfish <- readRDS(".../osmfish.rds")
```

Read multiple reference datasets.

```
#read the first reference
zeisel <- readRDS(".../zeisel.rds")

#read the second reference
allen_SSp <- readRDS(".../allen_SSp.rds")

#read the third reference
allen_Visp <- readRDS(".../allen_Visp.rds")
```

These multiple reference datasets should be put into a list as an input to ENGEP.

```
ref_list = list(zeisel,allen_SSp,allen_Visp)
```

Here, we predict the expression levels of the following three genes as an example.

```
pre_genes = c('Pvrl3','Wfs1','Cux2')
```

The predicted results can be obtained by running this function.

```
engep_predict <- engep_predict(osmfish,ref_list,pre_genes)
```

We can plot the expression patterns of these genes.

```
locations=read.csv('.../osmloc.csv',row.names = 1)
gene_expressions = as.data.frame(engep_predict)
locations = locations[rownames(gene_expressions),]

draw_grid(ncol(gene_expressions),locations,gene_expressions)
```

