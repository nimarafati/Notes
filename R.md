# dplyr 
## Select columns and present in `DT::datatable`
```
DT::datatable(select(.data = distinct(data.TMM_gene_biotype_filtered_goi), c(-sum_expression)), caption = 'Expression of genes of interest')   %>%
formatRound(columns=c('S_211', 'S_2211'), digits=2, interval = 0)
```

##
