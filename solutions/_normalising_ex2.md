In a typical differential expression analysis, the majority of the genes are assumed to be non-differentially expressed. For this reason, it is useful to examine boxplots of counts across samples in each dataset, both before and after normalization. An effective normalization should result in a stabilization of read count distributions across replicates.

```rconsole
# check this!!
# remember that we were working with a subset of the annotation
rpkm_chr4=rpkm
raw_counts_chr4=counts[row.names(counts) %in% row.names(rpkm_chr4),]
norm_counts_chr4=norm_counts[row.names(norm_counts) %in% row.names(rpkm_chr4),]

# create a list to simplify the plotting step
l=list(
        split(raw_counts_chr4, colnames(raw_counts_chr4)),
        split(rpkm_chr4, colnames(rpkm_chr4)),
        split(norm_counts_chr4, colnames(norm_counts_chr4))
)
names(l)=c("raw counts", "RPKMs", "normalised counts - DESeq")

# visualise the data as a set of boxplots
par(mfrow=c(1,3), las=2, mar=c(7,5,3,3), cex=1)
boxplot(l[[1]], outline=F, ylab="raw counts", ylim=c(0, 3500))
boxplot(l[[2]], outline=F, ylab="RPKMs", ylim=c(0, 50))
boxplot(l[[3]], outline=F, ylab="normalised counts - DESeq", ylim=c(0, 3500))
```