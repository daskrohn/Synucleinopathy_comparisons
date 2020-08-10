# Synucleinopathy_comparisons
Heatmap for later: https://jcoliver.github.io/learn-r/006-heatmaps.html

PD is the most genetically understood of the synucleinopathies (PD, DLB, MSA, RBD) because of the large sample sizes available for GWAS. For this reason, I've compared the results for the PD top GWAS hits in both RBD (current) and DLB (Scholz et. al.) GWAS.  

## Beta-Beta Plot

**Prepare:**
```R
setwd("~/Desktop/Projects/GWAS/beta-beta/")
data <- read.csv("RBD_GWAS_meta-5-comparisons.csv")
names(data)
attach(data)

require("ggplot2")
require("reshape2")
require("corrplot")
require("ggrepel")
```

### Create plots
**Idiopathic RBD:**
```R
png('iRBD_GWAS_beta-beta_tricolor.png', units="in", width=6, height=5, res=300, compression = 'lzw')

irbd <- ggplot(data, aes(x=Beta_Meta5, y=meta5_beta_adjusted_iRBD)) + geom_vline(xintercept = 0, colour = "grey") + 
  geom_hline(yintercept = 0, colour = "grey") +
 geom_point(shape = 16, size = 4, aes(color = Direction_compare_iRBD), alpha=0.7) + 
  xlim(-0.8, 0.8) 

irbd2 <- irbd + scale_color_manual(values = c("red2", "blue", "grey65"))

irbd3 <- irbd2 + geom_vline(xintercept = 0, colour = "grey") + geom_hline(yintercept = 0, colour = "grey") + theme_light()

irbd4 <- irbd3 +
  geom_label_repel(aes(label = NAME),
                   box.padding   = 0.35, 
                   point.padding = 0.5,
                   segment.color = 'grey50') 

irbd5 <- irbd4 + ggtitle("Beta-Beta Plot: PD vs iRBD") +
  xlab("PD Betas (Nalls et. al. 2019)") + ylab("RBD Betas (iRBD GWAS)") + theme(plot.title = element_text(face="bold"))

irbd5 + theme(legend.position = "none") + theme(plot.title = element_text(hjust = 0.5)) 

dev.off()
```
