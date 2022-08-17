`ridgeline_plot`  is used for visualising enrichment analysis results in DE analysis. Package `hrbrthemes` has dependecies on `systemfonts` which I installed as follows:  
```withr::with_makevars(c(OBJCXX = "gcc"), install.packages('systemfonts'))```

```ridgeline_plot <- function(ego_result, plot_name){
  library(ggridges)
  library(ggplot2)
  library(viridis)
  library(hrbrthemes)
  library(tidyr)
  library(dplyr)
  t <- ego_result
  t <- t %>% mutate(geneID = strsplit(as.character(geneID), '/')) %>% unnest(geneID) %>% filter(geneID != '') %>% dplyr::select(geneID, c('ONTOLOGY', 'Description', 'geneID'))
  t <- data.frame(t, logFC = fc_sorted[t$geneID])
  
  for(ont in unique(t$ONTOLOGY)){
    png(paste0(plot_name, '_', ont, '.png'), res = 200, height = 2000, width = 2000)
    p <- ggplot(t[(t$ONTOLOGY == ont),], aes(x = logFC, y = Description, fill = ..x..)) +
    geom_density_ridges_gradient(scale = 3, rel_min_height = 0.01) +
    scale_fill_viridis(name = "logFC", option = "C") +
    labs(title = paste0('logFC distribution of genes in enriched GO terms (', ont, ')')) +
    theme_ipsum() +
      theme(
        legend.position="none",
        panel.spacing = unit(0.1, "lines"),
        strip.text.x = element_text(size = 8)
      )
    print(p)
    dev.off()
  }
}```
