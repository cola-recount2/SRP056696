cola Report for recount2:SRP056696
==================

**Date**: 2019-12-26 00:53:47 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 17231    53
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[ATC:pam](#ATC-pam)         |          2| 1.000|           0.952|       0.980|** |           |
|[ATC:NMF](#ATC-NMF)         |          2| 1.000|           0.946|       0.979|** |           |
|[ATC:kmeans](#ATC-kmeans)   |          3| 0.971|           0.949|       0.979|** |2          |
|[ATC:skmeans](#ATC-skmeans) |          2| 0.960|           0.939|       0.976|** |           |
|[SD:skmeans](#SD-skmeans)   |          2| 0.847|           0.913|       0.965|   |           |
|[MAD:skmeans](#MAD-skmeans) |          2| 0.847|           0.891|       0.958|   |           |
|[CV:skmeans](#CV-skmeans)   |          3| 0.811|           0.876|       0.931|   |           |
|[SD:pam](#SD-pam)           |          5| 0.798|           0.787|       0.901|   |           |
|[SD:NMF](#SD-NMF)           |          3| 0.767|           0.842|       0.936|   |           |
|[MAD:NMF](#MAD-NMF)         |          3| 0.764|           0.849|       0.931|   |           |
|[ATC:hclust](#ATC-hclust)   |          2| 0.754|           0.832|       0.919|   |           |
|[MAD:pam](#MAD-pam)         |          5| 0.739|           0.715|       0.872|   |           |
|[CV:NMF](#CV-NMF)           |          2| 0.720|           0.885|       0.932|   |           |
|[CV:pam](#CV-pam)           |          2| 0.675|           0.826|       0.915|   |           |
|[MAD:kmeans](#MAD-kmeans)   |          2| 0.620|           0.790|       0.899|   |           |
|[CV:hclust](#CV-hclust)     |          5| 0.512|           0.295|       0.648|   |           |
|[SD:kmeans](#SD-kmeans)     |          2| 0.507|           0.688|       0.865|   |           |
|[SD:mclust](#SD-mclust)     |          2| 0.473|           0.799|       0.852|   |           |
|[SD:hclust](#SD-hclust)     |          4| 0.464|           0.491|       0.760|   |           |
|[CV:kmeans](#CV-kmeans)     |          4| 0.448|           0.556|       0.712|   |           |
|[ATC:mclust](#ATC-mclust)   |          4| 0.423|           0.470|       0.713|   |           |
|[MAD:hclust](#MAD-hclust)   |          3| 0.365|           0.721|       0.836|   |           |
|[MAD:mclust](#MAD-mclust)   |          2| 0.365|           0.669|       0.773|   |           |
|[CV:mclust](#CV-mclust)     |          3| 0.334|           0.661|       0.783|   |           |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 0.589           0.823       0.924          0.491 0.492   0.492
#&gt; CV:NMF      2 0.720           0.885       0.932          0.499 0.495   0.495
#&gt; MAD:NMF     2 0.611           0.806       0.918          0.491 0.495   0.495
#&gt; ATC:NMF     2 1.000           0.946       0.979          0.336 0.665   0.665
#&gt; SD:skmeans  2 0.847           0.913       0.965          0.509 0.491   0.491
#&gt; CV:skmeans  2 0.463           0.794       0.867          0.497 0.505   0.505
#&gt; MAD:skmeans 2 0.847           0.891       0.958          0.509 0.491   0.491
#&gt; ATC:skmeans 2 0.960           0.939       0.976          0.502 0.499   0.499
#&gt; SD:mclust   2 0.473           0.799       0.852          0.397 0.643   0.643
#&gt; CV:mclust   2 0.484           0.876       0.905          0.309 0.713   0.713
#&gt; MAD:mclust  2 0.365           0.669       0.773          0.389 0.643   0.643
#&gt; ATC:mclust  2 0.463           0.793       0.862          0.324 0.766   0.766
#&gt; SD:kmeans   2 0.507           0.688       0.865          0.474 0.505   0.505
#&gt; CV:kmeans   2 0.220           0.651       0.822          0.422 0.570   0.570
#&gt; MAD:kmeans  2 0.620           0.790       0.899          0.494 0.495   0.495
#&gt; ATC:kmeans  2 1.000           0.990       0.995          0.442 0.556   0.556
#&gt; SD:pam      2 0.418           0.692       0.876          0.437 0.586   0.586
#&gt; CV:pam      2 0.675           0.826       0.915          0.503 0.491   0.491
#&gt; MAD:pam     2 0.569           0.861       0.933          0.404 0.623   0.623
#&gt; ATC:pam     2 1.000           0.952       0.980          0.369 0.623   0.623
#&gt; SD:hclust   2 0.496           0.857       0.910          0.272 0.713   0.713
#&gt; CV:hclust   2 0.562           0.729       0.840          0.235 0.795   0.795
#&gt; MAD:hclust  2 0.322           0.847       0.822          0.331 0.713   0.713
#&gt; ATC:hclust  2 0.754           0.832       0.919          0.412 0.604   0.604
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.767           0.842       0.936          0.308 0.647   0.410
#&gt; CV:NMF      3 0.607           0.748       0.857          0.328 0.718   0.491
#&gt; MAD:NMF     3 0.764           0.849       0.931          0.299 0.641   0.414
#&gt; ATC:NMF     3 0.607           0.705       0.883          0.845 0.637   0.487
#&gt; SD:skmeans  3 0.618           0.773       0.868          0.323 0.683   0.440
#&gt; CV:skmeans  3 0.811           0.876       0.931          0.358 0.688   0.454
#&gt; MAD:skmeans 3 0.602           0.783       0.874          0.323 0.720   0.490
#&gt; ATC:skmeans 3 0.715           0.616       0.845          0.286 0.808   0.630
#&gt; SD:mclust   3 0.214           0.581       0.721          0.394 0.623   0.472
#&gt; CV:mclust   3 0.334           0.661       0.783          0.869 0.441   0.352
#&gt; MAD:mclust  3 0.172           0.283       0.617          0.331 0.556   0.441
#&gt; ATC:mclust  3 0.310           0.518       0.701          0.741 0.623   0.508
#&gt; SD:kmeans   3 0.376           0.302       0.561          0.334 0.756   0.588
#&gt; CV:kmeans   3 0.323           0.468       0.693          0.426 0.577   0.386
#&gt; MAD:kmeans  3 0.353           0.445       0.713          0.295 0.644   0.404
#&gt; ATC:kmeans  3 0.971           0.949       0.979          0.404 0.690   0.507
#&gt; SD:pam      3 0.412           0.590       0.797          0.465 0.692   0.500
#&gt; CV:pam      3 0.433           0.551       0.818          0.225 0.749   0.549
#&gt; MAD:pam     3 0.571           0.780       0.859          0.534 0.736   0.576
#&gt; ATC:pam     3 0.831           0.852       0.947          0.440 0.752   0.629
#&gt; SD:hclust   3 0.290           0.583       0.732          0.850 0.759   0.674
#&gt; CV:hclust   3 0.591           0.133       0.615          0.613 0.522   0.452
#&gt; MAD:hclust  3 0.365           0.721       0.836          0.642 0.708   0.590
#&gt; ATC:hclust  3 0.624           0.673       0.877          0.408 0.805   0.689
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.566           0.700       0.838         0.1332 0.744   0.416
#&gt; CV:NMF      4 0.577           0.712       0.829         0.1383 0.739   0.371
#&gt; MAD:NMF     4 0.557           0.707       0.841         0.1607 0.763   0.447
#&gt; ATC:NMF     4 0.689           0.788       0.891         0.1968 0.765   0.461
#&gt; SD:skmeans  4 0.593           0.624       0.782         0.1240 0.819   0.514
#&gt; CV:skmeans  4 0.642           0.610       0.799         0.1204 0.872   0.630
#&gt; MAD:skmeans 4 0.666           0.721       0.801         0.1256 0.800   0.477
#&gt; ATC:skmeans 4 0.871           0.860       0.929         0.1250 0.875   0.663
#&gt; SD:mclust   4 0.434           0.569       0.762         0.0830 0.592   0.309
#&gt; CV:mclust   4 0.376           0.696       0.754         0.1676 0.706   0.434
#&gt; MAD:mclust  4 0.571           0.810       0.892         0.1175 0.767   0.590
#&gt; ATC:mclust  4 0.423           0.470       0.713         0.1783 0.680   0.436
#&gt; SD:kmeans   4 0.473           0.433       0.670         0.1402 0.691   0.385
#&gt; CV:kmeans   4 0.448           0.556       0.712         0.1486 0.838   0.621
#&gt; MAD:kmeans  4 0.466           0.567       0.730         0.1384 0.737   0.396
#&gt; ATC:kmeans  4 0.593           0.543       0.742         0.1795 0.812   0.544
#&gt; SD:pam      4 0.569           0.752       0.849         0.0948 0.906   0.744
#&gt; CV:pam      4 0.629           0.647       0.847         0.0758 0.750   0.472
#&gt; MAD:pam     4 0.689           0.822       0.919         0.1134 0.811   0.555
#&gt; ATC:pam     4 0.609           0.598       0.838         0.2462 0.793   0.577
#&gt; SD:hclust   4 0.464           0.491       0.760         0.3054 0.620   0.377
#&gt; CV:hclust   4 0.600           0.707       0.850         0.2327 0.578   0.386
#&gt; MAD:hclust  4 0.525           0.677       0.798         0.2737 0.848   0.637
#&gt; ATC:hclust  4 0.527           0.677       0.796         0.1754 0.851   0.679
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.712           0.726       0.866         0.0977 0.759   0.320
#&gt; CV:NMF      5 0.746           0.640       0.838         0.0670 0.819   0.415
#&gt; MAD:NMF     5 0.784           0.764       0.884         0.0780 0.835   0.470
#&gt; ATC:NMF     5 0.658           0.691       0.818         0.0825 0.866   0.541
#&gt; SD:skmeans  5 0.673           0.663       0.812         0.0672 0.840   0.454
#&gt; CV:skmeans  5 0.660           0.649       0.787         0.0664 0.893   0.606
#&gt; MAD:skmeans 5 0.681           0.592       0.788         0.0654 0.896   0.608
#&gt; ATC:skmeans 5 0.798           0.719       0.865         0.0517 0.946   0.810
#&gt; SD:mclust   5 0.503           0.726       0.721         0.1745 0.797   0.496
#&gt; CV:mclust   5 0.590           0.535       0.721         0.0999 0.877   0.649
#&gt; MAD:mclust  5 0.474           0.602       0.773         0.2258 0.840   0.615
#&gt; ATC:mclust  5 0.384           0.397       0.617         0.1172 0.623   0.251
#&gt; SD:kmeans   5 0.578           0.584       0.671         0.0795 0.813   0.419
#&gt; CV:kmeans   5 0.491           0.495       0.585         0.0861 0.790   0.413
#&gt; MAD:kmeans  5 0.642           0.594       0.731         0.0786 0.833   0.496
#&gt; ATC:kmeans  5 0.599           0.478       0.681         0.0780 0.832   0.465
#&gt; SD:pam      5 0.798           0.787       0.901         0.1104 0.808   0.461
#&gt; CV:pam      5 0.746           0.812       0.905         0.1314 0.822   0.523
#&gt; MAD:pam     5 0.739           0.715       0.872         0.1166 0.877   0.621
#&gt; ATC:pam     5 0.737           0.724       0.881         0.1197 0.901   0.695
#&gt; SD:hclust   5 0.506           0.584       0.769         0.0801 0.936   0.804
#&gt; CV:hclust   5 0.512           0.295       0.648         0.3435 0.546   0.279
#&gt; MAD:hclust  5 0.594           0.690       0.816         0.0433 0.987   0.951
#&gt; ATC:hclust  5 0.594           0.469       0.721         0.1264 0.828   0.515
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.760           0.655       0.837         0.0479 0.884   0.509
#&gt; CV:NMF      6 0.861           0.793       0.900         0.0460 0.898   0.554
#&gt; MAD:NMF     6 0.739           0.578       0.798         0.0494 0.890   0.544
#&gt; ATC:NMF     6 0.722           0.627       0.753         0.0493 0.896   0.547
#&gt; SD:skmeans  6 0.725           0.646       0.764         0.0400 0.964   0.811
#&gt; CV:skmeans  6 0.711           0.556       0.753         0.0425 0.921   0.635
#&gt; MAD:skmeans 6 0.719           0.558       0.700         0.0405 0.898   0.547
#&gt; ATC:skmeans 6 0.761           0.681       0.833         0.0311 0.972   0.885
#&gt; SD:mclust   6 0.646           0.562       0.742         0.1154 0.848   0.550
#&gt; CV:mclust   6 0.633           0.691       0.733         0.0499 0.819   0.439
#&gt; MAD:mclust  6 0.656           0.624       0.762         0.0995 0.959   0.856
#&gt; ATC:mclust  6 0.552           0.461       0.720         0.0999 0.856   0.442
#&gt; SD:kmeans   6 0.740           0.653       0.789         0.0524 0.954   0.782
#&gt; CV:kmeans   6 0.529           0.474       0.593         0.0606 0.852   0.443
#&gt; MAD:kmeans  6 0.767           0.699       0.822         0.0512 0.909   0.628
#&gt; ATC:kmeans  6 0.651           0.405       0.633         0.0505 0.897   0.580
#&gt; SD:pam      6 0.768           0.738       0.886         0.0481 0.959   0.813
#&gt; CV:pam      6 0.806           0.816       0.913         0.0612 0.927   0.718
#&gt; MAD:pam     6 0.776           0.701       0.879         0.0540 0.910   0.643
#&gt; ATC:pam     6 0.692           0.722       0.848         0.0564 0.959   0.837
#&gt; SD:hclust   6 0.683           0.658       0.765         0.0970 0.906   0.661
#&gt; CV:hclust   6 0.544           0.685       0.765         0.1214 0.739   0.400
#&gt; MAD:hclust  6 0.710           0.576       0.743         0.0926 0.814   0.430
#&gt; ATC:hclust  6 0.678           0.598       0.765         0.0708 0.947   0.761
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.496           0.857       0.910         0.2717 0.713   0.713
#> 3 3 0.290           0.583       0.732         0.8501 0.759   0.674
#> 4 4 0.464           0.491       0.760         0.3054 0.620   0.377
#> 5 5 0.506           0.584       0.769         0.0801 0.936   0.804
#> 6 6 0.683           0.658       0.765         0.0970 0.906   0.661
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1  0.3733      0.881 0.928 0.072
#&gt; SRR1946691     2  0.9460      0.730 0.364 0.636
#&gt; SRR1946690     2  0.9323      0.760 0.348 0.652
#&gt; SRR1946689     2  0.0938      0.689 0.012 0.988
#&gt; SRR1946686     1  0.3733      0.881 0.928 0.072
#&gt; SRR1946685     1  0.4431      0.875 0.908 0.092
#&gt; SRR1946688     1  0.5408      0.850 0.876 0.124
#&gt; SRR1946684     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946683     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946682     1  0.2603      0.907 0.956 0.044
#&gt; SRR1946680     2  0.0938      0.689 0.012 0.988
#&gt; SRR1946681     2  0.9358      0.758 0.352 0.648
#&gt; SRR1946687     1  0.3733      0.881 0.928 0.072
#&gt; SRR1946679     1  0.4431      0.875 0.908 0.092
#&gt; SRR1946678     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946676     1  0.2423      0.908 0.960 0.040
#&gt; SRR1946677     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946672     1  0.5842      0.794 0.860 0.140
#&gt; SRR1946673     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946671     1  0.0000      0.917 1.000 0.000
#&gt; SRR1946669     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946668     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946666     1  0.3733      0.881 0.928 0.072
#&gt; SRR1946667     2  0.0938      0.689 0.012 0.988
#&gt; SRR1946670     1  0.5059      0.858 0.888 0.112
#&gt; SRR1946663     1  0.2603      0.907 0.956 0.044
#&gt; SRR1946664     2  0.9323      0.760 0.348 0.652
#&gt; SRR1946662     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946661     1  0.0000      0.917 1.000 0.000
#&gt; SRR1946660     1  0.5408      0.850 0.876 0.124
#&gt; SRR1946659     1  0.3733      0.881 0.928 0.072
#&gt; SRR1946658     1  0.5059      0.858 0.888 0.112
#&gt; SRR1946657     1  0.4939      0.861 0.892 0.108
#&gt; SRR1946655     1  0.8861      0.516 0.696 0.304
#&gt; SRR1946654     1  0.6148      0.782 0.848 0.152
#&gt; SRR1946653     1  0.3733      0.881 0.928 0.072
#&gt; SRR1946652     1  0.4161      0.882 0.916 0.084
#&gt; SRR1946651     1  0.4562      0.872 0.904 0.096
#&gt; SRR1946650     1  0.0672      0.917 0.992 0.008
#&gt; SRR1946649     1  0.0000      0.917 1.000 0.000
#&gt; SRR1946648     1  0.4022      0.884 0.920 0.080
#&gt; SRR1946647     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946646     1  0.4690      0.873 0.900 0.100
#&gt; SRR1946645     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946644     1  0.5178      0.858 0.884 0.116
#&gt; SRR1946643     2  0.9358      0.758 0.352 0.648
#&gt; SRR1946642     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946641     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946656     2  0.9358      0.758 0.352 0.648
#&gt; SRR1946640     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946639     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946638     1  0.0938      0.917 0.988 0.012
#&gt; SRR1946637     1  0.0938      0.917 0.988 0.012
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     2  0.6585     0.6652 0.244 0.712 0.044
#&gt; SRR1946691     2  0.8637    -0.7051 0.100 0.456 0.444
#&gt; SRR1946690     3  0.8523     0.6901 0.092 0.444 0.464
#&gt; SRR1946689     3  0.0000     0.5547 0.000 0.000 1.000
#&gt; SRR1946686     2  0.6585     0.6652 0.244 0.712 0.044
#&gt; SRR1946685     2  0.0237     0.6916 0.004 0.996 0.000
#&gt; SRR1946688     2  0.2414     0.6824 0.040 0.940 0.020
#&gt; SRR1946684     2  0.6305     0.0687 0.484 0.516 0.000
#&gt; SRR1946683     2  0.6079     0.3644 0.388 0.612 0.000
#&gt; SRR1946682     2  0.3454     0.7160 0.104 0.888 0.008
#&gt; SRR1946680     3  0.0000     0.5547 0.000 0.000 1.000
#&gt; SRR1946681     3  0.8691     0.6873 0.104 0.444 0.452
#&gt; SRR1946687     2  0.6585     0.6652 0.244 0.712 0.044
#&gt; SRR1946679     2  0.0237     0.6916 0.004 0.996 0.000
#&gt; SRR1946678     1  0.3686     0.9139 0.860 0.140 0.000
#&gt; SRR1946676     2  0.2796     0.7168 0.092 0.908 0.000
#&gt; SRR1946677     2  0.6062     0.3703 0.384 0.616 0.000
#&gt; SRR1946672     2  0.6970     0.6406 0.276 0.676 0.048
#&gt; SRR1946673     2  0.6305     0.0687 0.484 0.516 0.000
#&gt; SRR1946671     2  0.3752     0.7044 0.144 0.856 0.000
#&gt; SRR1946669     1  0.6260     0.1160 0.552 0.448 0.000
#&gt; SRR1946668     2  0.6305     0.0687 0.484 0.516 0.000
#&gt; SRR1946666     2  0.6585     0.6652 0.244 0.712 0.044
#&gt; SRR1946667     3  0.0000     0.5547 0.000 0.000 1.000
#&gt; SRR1946670     2  0.1950     0.6874 0.040 0.952 0.008
#&gt; SRR1946663     2  0.3454     0.7160 0.104 0.888 0.008
#&gt; SRR1946664     3  0.8523     0.6901 0.092 0.444 0.464
#&gt; SRR1946662     2  0.6305     0.0687 0.484 0.516 0.000
#&gt; SRR1946661     2  0.3816     0.7025 0.148 0.852 0.000
#&gt; SRR1946660     2  0.2414     0.6824 0.040 0.940 0.020
#&gt; SRR1946659     2  0.6585     0.6652 0.244 0.712 0.044
#&gt; SRR1946658     2  0.1950     0.6874 0.040 0.952 0.008
#&gt; SRR1946657     2  0.0592     0.6763 0.012 0.988 0.000
#&gt; SRR1946655     2  0.6091     0.3967 0.124 0.784 0.092
#&gt; SRR1946654     2  0.6937     0.6384 0.272 0.680 0.048
#&gt; SRR1946653     2  0.6585     0.6652 0.244 0.712 0.044
#&gt; SRR1946652     2  0.0747     0.7005 0.016 0.984 0.000
#&gt; SRR1946651     2  0.0000     0.6880 0.000 1.000 0.000
#&gt; SRR1946650     2  0.3482     0.7097 0.128 0.872 0.000
#&gt; SRR1946649     2  0.3752     0.7041 0.144 0.856 0.000
#&gt; SRR1946648     2  0.7476     0.2950 0.452 0.512 0.036
#&gt; SRR1946647     2  0.6305     0.0687 0.484 0.516 0.000
#&gt; SRR1946646     2  0.0829     0.6896 0.012 0.984 0.004
#&gt; SRR1946645     2  0.6079     0.3644 0.388 0.612 0.000
#&gt; SRR1946644     2  0.1129     0.6732 0.020 0.976 0.004
#&gt; SRR1946643     3  0.8691     0.6873 0.104 0.444 0.452
#&gt; SRR1946642     1  0.3551     0.9222 0.868 0.132 0.000
#&gt; SRR1946641     1  0.3551     0.9222 0.868 0.132 0.000
#&gt; SRR1946656     3  0.8691     0.6873 0.104 0.444 0.452
#&gt; SRR1946640     1  0.3551     0.9222 0.868 0.132 0.000
#&gt; SRR1946639     1  0.3551     0.9222 0.868 0.132 0.000
#&gt; SRR1946638     1  0.3551     0.9222 0.868 0.132 0.000
#&gt; SRR1946637     1  0.3551     0.9222 0.868 0.132 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.6162      0.647 0.304 0.076 0.620 0.000
#&gt; SRR1946691     2  0.7803     -0.186 0.008 0.460 0.196 0.336
#&gt; SRR1946690     2  0.8162     -0.226 0.008 0.368 0.288 0.336
#&gt; SRR1946689     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1946686     3  0.6162      0.647 0.304 0.076 0.620 0.000
#&gt; SRR1946685     2  0.2179      0.713 0.012 0.924 0.064 0.000
#&gt; SRR1946688     2  0.1471      0.704 0.004 0.960 0.024 0.012
#&gt; SRR1946684     1  0.4941      0.419 0.564 0.436 0.000 0.000
#&gt; SRR1946683     2  0.6661     -0.308 0.456 0.460 0.084 0.000
#&gt; SRR1946682     2  0.2480      0.680 0.088 0.904 0.008 0.000
#&gt; SRR1946680     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1946681     3  0.5180     -0.051 0.004 0.016 0.672 0.308
#&gt; SRR1946687     3  0.6162      0.647 0.304 0.076 0.620 0.000
#&gt; SRR1946679     2  0.2179      0.713 0.012 0.924 0.064 0.000
#&gt; SRR1946678     1  0.0592      0.613 0.984 0.016 0.000 0.000
#&gt; SRR1946676     2  0.2675      0.688 0.100 0.892 0.008 0.000
#&gt; SRR1946677     2  0.6661     -0.308 0.456 0.460 0.084 0.000
#&gt; SRR1946672     3  0.5690      0.653 0.216 0.084 0.700 0.000
#&gt; SRR1946673     1  0.4941      0.419 0.564 0.436 0.000 0.000
#&gt; SRR1946671     2  0.3074      0.640 0.152 0.848 0.000 0.000
#&gt; SRR1946669     1  0.4746      0.482 0.632 0.368 0.000 0.000
#&gt; SRR1946668     1  0.4941      0.419 0.564 0.436 0.000 0.000
#&gt; SRR1946666     3  0.6162      0.647 0.304 0.076 0.620 0.000
#&gt; SRR1946667     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1946670     2  0.1004      0.707 0.004 0.972 0.024 0.000
#&gt; SRR1946663     2  0.2480      0.680 0.088 0.904 0.008 0.000
#&gt; SRR1946664     2  0.8162     -0.226 0.008 0.368 0.288 0.336
#&gt; SRR1946662     1  0.4941      0.419 0.564 0.436 0.000 0.000
#&gt; SRR1946661     2  0.3172      0.632 0.160 0.840 0.000 0.000
#&gt; SRR1946660     2  0.1471      0.704 0.004 0.960 0.024 0.012
#&gt; SRR1946659     3  0.6162      0.647 0.304 0.076 0.620 0.000
#&gt; SRR1946658     2  0.1004      0.707 0.004 0.972 0.024 0.000
#&gt; SRR1946657     2  0.2342      0.709 0.008 0.912 0.080 0.000
#&gt; SRR1946655     3  0.2081      0.484 0.000 0.084 0.916 0.000
#&gt; SRR1946654     3  0.5690      0.650 0.196 0.096 0.708 0.000
#&gt; SRR1946653     3  0.6162      0.647 0.304 0.076 0.620 0.000
#&gt; SRR1946652     2  0.2197      0.714 0.024 0.928 0.048 0.000
#&gt; SRR1946651     2  0.2048      0.712 0.008 0.928 0.064 0.000
#&gt; SRR1946650     2  0.2814      0.660 0.132 0.868 0.000 0.000
#&gt; SRR1946649     2  0.3074      0.641 0.152 0.848 0.000 0.000
#&gt; SRR1946648     1  0.6568     -0.120 0.512 0.080 0.408 0.000
#&gt; SRR1946647     1  0.4941      0.419 0.564 0.436 0.000 0.000
#&gt; SRR1946646     2  0.3708      0.671 0.020 0.832 0.148 0.000
#&gt; SRR1946645     2  0.6661     -0.308 0.456 0.460 0.084 0.000
#&gt; SRR1946644     2  0.3790      0.664 0.016 0.820 0.164 0.000
#&gt; SRR1946643     3  0.5180     -0.051 0.004 0.016 0.672 0.308
#&gt; SRR1946642     1  0.0336      0.612 0.992 0.008 0.000 0.000
#&gt; SRR1946641     1  0.0336      0.612 0.992 0.008 0.000 0.000
#&gt; SRR1946656     3  0.5180     -0.051 0.004 0.016 0.672 0.308
#&gt; SRR1946640     1  0.0336      0.612 0.992 0.008 0.000 0.000
#&gt; SRR1946639     1  0.0336      0.612 0.992 0.008 0.000 0.000
#&gt; SRR1946638     1  0.0336      0.612 0.992 0.008 0.000 0.000
#&gt; SRR1946637     1  0.0336      0.612 0.992 0.008 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5
#&gt; SRR1946675     3  0.3480     0.7178 0.248 0.000 0.752  0 0.000
#&gt; SRR1946691     2  0.3530     0.8775 0.000 0.784 0.012  0 0.204
#&gt; SRR1946690     2  0.4342     0.9398 0.000 0.728 0.040  0 0.232
#&gt; SRR1946689     4  0.0000     1.0000 0.000 0.000 0.000  1 0.000
#&gt; SRR1946686     3  0.3480     0.7178 0.248 0.000 0.752  0 0.000
#&gt; SRR1946685     5  0.0960     0.7558 0.004 0.016 0.008  0 0.972
#&gt; SRR1946688     5  0.3720     0.7154 0.000 0.228 0.012  0 0.760
#&gt; SRR1946684     1  0.4430     0.3287 0.540 0.004 0.000  0 0.456
#&gt; SRR1946683     5  0.6320    -0.0962 0.388 0.008 0.124  0 0.480
#&gt; SRR1946682     5  0.4573     0.7164 0.032 0.232 0.012  0 0.724
#&gt; SRR1946680     4  0.0000     1.0000 0.000 0.000 0.000  1 0.000
#&gt; SRR1946681     3  0.4291    -0.1387 0.000 0.464 0.536  0 0.000
#&gt; SRR1946687     3  0.3480     0.7178 0.248 0.000 0.752  0 0.000
#&gt; SRR1946679     5  0.0960     0.7558 0.004 0.016 0.008  0 0.972
#&gt; SRR1946678     1  0.0693     0.5961 0.980 0.000 0.012  0 0.008
#&gt; SRR1946676     5  0.1831     0.7534 0.076 0.004 0.000  0 0.920
#&gt; SRR1946677     5  0.6633    -0.0605 0.368 0.024 0.124  0 0.484
#&gt; SRR1946672     3  0.4204     0.6952 0.196 0.048 0.756  0 0.000
#&gt; SRR1946673     1  0.4430     0.3287 0.540 0.004 0.000  0 0.456
#&gt; SRR1946671     5  0.2733     0.7282 0.112 0.012 0.004  0 0.872
#&gt; SRR1946669     1  0.4299     0.4164 0.608 0.004 0.000  0 0.388
#&gt; SRR1946668     1  0.4425     0.3316 0.544 0.004 0.000  0 0.452
#&gt; SRR1946666     3  0.3480     0.7178 0.248 0.000 0.752  0 0.000
#&gt; SRR1946667     4  0.0000     1.0000 0.000 0.000 0.000  1 0.000
#&gt; SRR1946670     5  0.3596     0.7276 0.000 0.212 0.012  0 0.776
#&gt; SRR1946663     5  0.4573     0.7164 0.032 0.232 0.012  0 0.724
#&gt; SRR1946664     2  0.4342     0.9398 0.000 0.728 0.040  0 0.232
#&gt; SRR1946662     1  0.4430     0.3287 0.540 0.004 0.000  0 0.456
#&gt; SRR1946661     5  0.2972     0.7304 0.108 0.024 0.004  0 0.864
#&gt; SRR1946660     5  0.3720     0.7154 0.000 0.228 0.012  0 0.760
#&gt; SRR1946659     3  0.3480     0.7178 0.248 0.000 0.752  0 0.000
#&gt; SRR1946658     5  0.3596     0.7276 0.000 0.212 0.012  0 0.776
#&gt; SRR1946657     5  0.1211     0.7479 0.000 0.024 0.016  0 0.960
#&gt; SRR1946655     3  0.1544     0.4878 0.000 0.068 0.932  0 0.000
#&gt; SRR1946654     3  0.4476     0.6822 0.172 0.048 0.764  0 0.016
#&gt; SRR1946653     3  0.3480     0.7178 0.248 0.000 0.752  0 0.000
#&gt; SRR1946652     5  0.1306     0.7619 0.016 0.016 0.008  0 0.960
#&gt; SRR1946651     5  0.0798     0.7532 0.000 0.016 0.008  0 0.976
#&gt; SRR1946650     5  0.2645     0.7533 0.068 0.044 0.000  0 0.888
#&gt; SRR1946649     5  0.2722     0.7245 0.120 0.008 0.004  0 0.868
#&gt; SRR1946648     3  0.5039     0.2725 0.456 0.000 0.512  0 0.032
#&gt; SRR1946647     1  0.4430     0.3287 0.540 0.004 0.000  0 0.456
#&gt; SRR1946646     5  0.2804     0.7202 0.012 0.016 0.092  0 0.880
#&gt; SRR1946645     5  0.6320    -0.0962 0.388 0.008 0.124  0 0.480
#&gt; SRR1946644     5  0.2990     0.7092 0.008 0.024 0.100  0 0.868
#&gt; SRR1946643     3  0.4291    -0.1387 0.000 0.464 0.536  0 0.000
#&gt; SRR1946642     1  0.0404     0.5942 0.988 0.000 0.012  0 0.000
#&gt; SRR1946641     1  0.0609     0.5933 0.980 0.000 0.020  0 0.000
#&gt; SRR1946656     3  0.4291    -0.1387 0.000 0.464 0.536  0 0.000
#&gt; SRR1946640     1  0.0609     0.5933 0.980 0.000 0.020  0 0.000
#&gt; SRR1946639     1  0.0609     0.5933 0.980 0.000 0.020  0 0.000
#&gt; SRR1946638     1  0.0609     0.5933 0.980 0.000 0.020  0 0.000
#&gt; SRR1946637     1  0.0609     0.5933 0.980 0.000 0.020  0 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5    p6
#&gt; SRR1946675     3  0.2048      0.838 0.120 0.000 0.880  0 0.000 0.000
#&gt; SRR1946691     5  0.4141      0.540 0.000 0.092 0.000  0 0.740 0.168
#&gt; SRR1946690     5  0.3717      0.567 0.000 0.148 0.000  0 0.780 0.072
#&gt; SRR1946689     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946686     3  0.2048      0.838 0.120 0.000 0.880  0 0.000 0.000
#&gt; SRR1946685     2  0.0291      0.782 0.004 0.992 0.000  0 0.004 0.000
#&gt; SRR1946688     6  0.3200      0.947 0.000 0.196 0.000  0 0.016 0.788
#&gt; SRR1946684     1  0.3833      0.283 0.556 0.444 0.000  0 0.000 0.000
#&gt; SRR1946683     2  0.6088      0.130 0.308 0.464 0.220  0 0.000 0.008
#&gt; SRR1946682     6  0.4271      0.911 0.036 0.180 0.036  0 0.000 0.748
#&gt; SRR1946680     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946681     5  0.5198      0.614 0.000 0.000 0.204  0 0.616 0.180
#&gt; SRR1946687     3  0.2048      0.838 0.120 0.000 0.880  0 0.000 0.000
#&gt; SRR1946679     2  0.0291      0.782 0.004 0.992 0.000  0 0.004 0.000
#&gt; SRR1946678     1  0.1643      0.604 0.924 0.008 0.068  0 0.000 0.000
#&gt; SRR1946676     2  0.1970      0.783 0.060 0.912 0.028  0 0.000 0.000
#&gt; SRR1946677     2  0.6130      0.147 0.320 0.464 0.204  0 0.000 0.012
#&gt; SRR1946672     3  0.5322      0.685 0.104 0.000 0.676  0 0.052 0.168
#&gt; SRR1946673     1  0.3833      0.283 0.556 0.444 0.000  0 0.000 0.000
#&gt; SRR1946671     2  0.2933      0.760 0.108 0.852 0.032  0 0.000 0.008
#&gt; SRR1946669     1  0.3695      0.372 0.624 0.376 0.000  0 0.000 0.000
#&gt; SRR1946668     1  0.4238      0.296 0.540 0.444 0.016  0 0.000 0.000
#&gt; SRR1946666     3  0.2048      0.838 0.120 0.000 0.880  0 0.000 0.000
#&gt; SRR1946667     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946670     6  0.2762      0.951 0.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1946663     6  0.4271      0.911 0.036 0.180 0.036  0 0.000 0.748
#&gt; SRR1946664     5  0.3717      0.567 0.000 0.148 0.000  0 0.780 0.072
#&gt; SRR1946662     1  0.3833      0.283 0.556 0.444 0.000  0 0.000 0.000
#&gt; SRR1946661     2  0.3127      0.758 0.104 0.844 0.040  0 0.000 0.012
#&gt; SRR1946660     6  0.3200      0.947 0.000 0.196 0.000  0 0.016 0.788
#&gt; SRR1946659     3  0.2048      0.838 0.120 0.000 0.880  0 0.000 0.000
#&gt; SRR1946658     6  0.2762      0.951 0.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1946657     2  0.0820      0.770 0.000 0.972 0.000  0 0.016 0.012
#&gt; SRR1946655     3  0.5270      0.252 0.000 0.000 0.604  0 0.216 0.180
#&gt; SRR1946654     3  0.5646      0.665 0.092 0.016 0.668  0 0.052 0.172
#&gt; SRR1946653     3  0.2048      0.838 0.120 0.000 0.880  0 0.000 0.000
#&gt; SRR1946652     2  0.0363      0.785 0.012 0.988 0.000  0 0.000 0.000
#&gt; SRR1946651     2  0.0146      0.780 0.000 0.996 0.000  0 0.004 0.000
#&gt; SRR1946650     2  0.2924      0.765 0.084 0.864 0.028  0 0.000 0.024
#&gt; SRR1946649     2  0.2981      0.761 0.100 0.852 0.040  0 0.000 0.008
#&gt; SRR1946648     3  0.4234      0.500 0.324 0.032 0.644  0 0.000 0.000
#&gt; SRR1946647     1  0.3833      0.283 0.556 0.444 0.000  0 0.000 0.000
#&gt; SRR1946646     2  0.2110      0.741 0.012 0.900 0.084  0 0.004 0.000
#&gt; SRR1946645     2  0.6080      0.125 0.312 0.464 0.216  0 0.000 0.008
#&gt; SRR1946644     2  0.2670      0.727 0.008 0.880 0.084  0 0.016 0.012
#&gt; SRR1946643     5  0.5198      0.614 0.000 0.000 0.204  0 0.616 0.180
#&gt; SRR1946642     1  0.1387      0.603 0.932 0.000 0.068  0 0.000 0.000
#&gt; SRR1946641     1  0.1501      0.601 0.924 0.000 0.076  0 0.000 0.000
#&gt; SRR1946656     5  0.5198      0.614 0.000 0.000 0.204  0 0.616 0.180
#&gt; SRR1946640     1  0.1501      0.601 0.924 0.000 0.076  0 0.000 0.000
#&gt; SRR1946639     1  0.1501      0.601 0.924 0.000 0.076  0 0.000 0.000
#&gt; SRR1946638     1  0.1501      0.601 0.924 0.000 0.076  0 0.000 0.000
#&gt; SRR1946637     1  0.1501      0.601 0.924 0.000 0.076  0 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.507           0.688       0.865         0.4745 0.505   0.505
#> 3 3 0.376           0.302       0.561         0.3344 0.756   0.588
#> 4 4 0.473           0.433       0.670         0.1402 0.691   0.385
#> 5 5 0.578           0.584       0.671         0.0795 0.813   0.419
#> 6 6 0.740           0.653       0.789         0.0524 0.954   0.782
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1   0.946     0.4531 0.636 0.364
#&gt; SRR1946691     2   0.388     0.8326 0.076 0.924
#&gt; SRR1946690     2   0.388     0.8326 0.076 0.924
#&gt; SRR1946689     2   0.000     0.8152 0.000 1.000
#&gt; SRR1946686     1   0.311     0.8305 0.944 0.056
#&gt; SRR1946685     1   0.991     0.0503 0.556 0.444
#&gt; SRR1946688     2   0.430     0.8326 0.088 0.912
#&gt; SRR1946684     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946683     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946682     1   0.992     0.0706 0.552 0.448
#&gt; SRR1946680     2   0.000     0.8152 0.000 1.000
#&gt; SRR1946681     2   0.358     0.8333 0.068 0.932
#&gt; SRR1946687     1   0.969     0.3731 0.604 0.396
#&gt; SRR1946679     2   0.991     0.3145 0.444 0.556
#&gt; SRR1946678     1   0.141     0.8405 0.980 0.020
#&gt; SRR1946676     1   0.991     0.0503 0.556 0.444
#&gt; SRR1946677     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946672     2   0.997     0.0605 0.468 0.532
#&gt; SRR1946673     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946671     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946669     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946668     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946666     1   0.311     0.8305 0.944 0.056
#&gt; SRR1946667     2   0.000     0.8152 0.000 1.000
#&gt; SRR1946670     2   0.430     0.8326 0.088 0.912
#&gt; SRR1946663     1   0.788     0.6228 0.764 0.236
#&gt; SRR1946664     2   0.388     0.8326 0.076 0.924
#&gt; SRR1946662     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946661     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946660     2   0.430     0.8326 0.088 0.912
#&gt; SRR1946659     1   0.311     0.8305 0.944 0.056
#&gt; SRR1946658     2   0.430     0.8326 0.088 0.912
#&gt; SRR1946657     2   0.788     0.7146 0.236 0.764
#&gt; SRR1946655     2   0.141     0.8243 0.020 0.980
#&gt; SRR1946654     2   0.943     0.3948 0.360 0.640
#&gt; SRR1946653     2   0.998     0.0438 0.472 0.528
#&gt; SRR1946652     1   0.991     0.0503 0.556 0.444
#&gt; SRR1946651     2   0.949     0.5079 0.368 0.632
#&gt; SRR1946650     1   0.844     0.5331 0.728 0.272
#&gt; SRR1946649     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946648     1   0.767     0.6845 0.776 0.224
#&gt; SRR1946647     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946646     2   0.714     0.7043 0.196 0.804
#&gt; SRR1946645     1   0.000     0.8428 1.000 0.000
#&gt; SRR1946644     2   0.327     0.8340 0.060 0.940
#&gt; SRR1946643     2   0.141     0.8243 0.020 0.980
#&gt; SRR1946642     1   0.141     0.8405 0.980 0.020
#&gt; SRR1946641     1   0.311     0.8305 0.944 0.056
#&gt; SRR1946656     2   0.141     0.8243 0.020 0.980
#&gt; SRR1946640     1   0.311     0.8305 0.944 0.056
#&gt; SRR1946639     1   0.311     0.8305 0.944 0.056
#&gt; SRR1946638     1   0.311     0.8305 0.944 0.056
#&gt; SRR1946637     1   0.311     0.8305 0.944 0.056
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.8985     0.8043 0.300 0.160 0.540
#&gt; SRR1946691     2  0.0829     0.5299 0.012 0.984 0.004
#&gt; SRR1946690     2  0.1999     0.5320 0.012 0.952 0.036
#&gt; SRR1946689     2  0.6168     0.2477 0.000 0.588 0.412
#&gt; SRR1946686     1  0.6204     0.1656 0.576 0.000 0.424
#&gt; SRR1946685     1  0.9147    -0.1229 0.444 0.412 0.144
#&gt; SRR1946688     2  0.4409     0.5192 0.172 0.824 0.004
#&gt; SRR1946684     1  0.1315     0.4472 0.972 0.008 0.020
#&gt; SRR1946683     1  0.1267     0.4376 0.972 0.004 0.024
#&gt; SRR1946682     2  0.6373     0.2420 0.408 0.588 0.004
#&gt; SRR1946680     2  0.6168     0.2477 0.000 0.588 0.412
#&gt; SRR1946681     2  0.6126     0.3336 0.004 0.644 0.352
#&gt; SRR1946687     3  0.9106     0.7228 0.336 0.156 0.508
#&gt; SRR1946679     1  0.9147    -0.1229 0.444 0.412 0.144
#&gt; SRR1946678     1  0.6168     0.2322 0.588 0.000 0.412
#&gt; SRR1946676     1  0.9147    -0.1229 0.444 0.412 0.144
#&gt; SRR1946677     1  0.2050     0.4298 0.952 0.028 0.020
#&gt; SRR1946672     3  0.8688     0.8290 0.196 0.208 0.596
#&gt; SRR1946673     1  0.3129     0.3990 0.904 0.088 0.008
#&gt; SRR1946671     1  0.2947     0.4217 0.920 0.020 0.060
#&gt; SRR1946669     1  0.1529     0.4405 0.960 0.000 0.040
#&gt; SRR1946668     1  0.0237     0.4458 0.996 0.000 0.004
#&gt; SRR1946666     1  0.6215     0.1465 0.572 0.000 0.428
#&gt; SRR1946667     2  0.6168     0.2477 0.000 0.588 0.412
#&gt; SRR1946670     2  0.4465     0.5179 0.176 0.820 0.004
#&gt; SRR1946663     2  0.6489     0.1543 0.456 0.540 0.004
#&gt; SRR1946664     2  0.1999     0.5320 0.012 0.952 0.036
#&gt; SRR1946662     1  0.1315     0.4472 0.972 0.008 0.020
#&gt; SRR1946661     1  0.6651     0.1825 0.640 0.340 0.020
#&gt; SRR1946660     2  0.4784     0.5078 0.200 0.796 0.004
#&gt; SRR1946659     1  0.6309     0.0396 0.504 0.000 0.496
#&gt; SRR1946658     2  0.6443     0.4710 0.240 0.720 0.040
#&gt; SRR1946657     1  0.9108    -0.1274 0.444 0.416 0.140
#&gt; SRR1946655     2  0.7075     0.1280 0.020 0.496 0.484
#&gt; SRR1946654     3  0.8803     0.7518 0.180 0.240 0.580
#&gt; SRR1946653     3  0.8834     0.8471 0.224 0.196 0.580
#&gt; SRR1946652     1  0.9147    -0.1229 0.444 0.412 0.144
#&gt; SRR1946651     1  0.9108    -0.1274 0.444 0.416 0.140
#&gt; SRR1946650     1  0.7990    -0.0116 0.532 0.404 0.064
#&gt; SRR1946649     1  0.2297     0.4293 0.944 0.036 0.020
#&gt; SRR1946648     1  0.8373    -0.4122 0.524 0.088 0.388
#&gt; SRR1946647     1  0.0237     0.4439 0.996 0.000 0.004
#&gt; SRR1946646     2  0.8307     0.3763 0.192 0.632 0.176
#&gt; SRR1946645     1  0.4345     0.3632 0.848 0.016 0.136
#&gt; SRR1946644     2  0.6546     0.4570 0.096 0.756 0.148
#&gt; SRR1946643     2  0.6819     0.1612 0.012 0.512 0.476
#&gt; SRR1946642     1  0.6168     0.2322 0.588 0.000 0.412
#&gt; SRR1946641     1  0.6168     0.2322 0.588 0.000 0.412
#&gt; SRR1946656     2  0.6819     0.1612 0.012 0.512 0.476
#&gt; SRR1946640     1  0.6168     0.2322 0.588 0.000 0.412
#&gt; SRR1946639     1  0.6168     0.2322 0.588 0.000 0.412
#&gt; SRR1946638     1  0.6168     0.2322 0.588 0.000 0.412
#&gt; SRR1946637     1  0.6168     0.2322 0.588 0.000 0.412
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3   0.798     0.3646 0.168 0.112 0.600 0.120
#&gt; SRR1946691     4   0.888     0.5835 0.196 0.068 0.320 0.416
#&gt; SRR1946690     4   0.881     0.5503 0.184 0.064 0.352 0.400
#&gt; SRR1946689     4   0.228     0.2103 0.000 0.000 0.096 0.904
#&gt; SRR1946686     1   0.754     0.4048 0.444 0.192 0.364 0.000
#&gt; SRR1946685     2   0.741     0.3608 0.172 0.464 0.364 0.000
#&gt; SRR1946688     4   0.944     0.5814 0.196 0.124 0.308 0.372
#&gt; SRR1946684     2   0.265     0.5963 0.108 0.888 0.004 0.000
#&gt; SRR1946683     2   0.252     0.6373 0.024 0.912 0.064 0.000
#&gt; SRR1946682     2   0.855     0.1868 0.196 0.512 0.072 0.220
#&gt; SRR1946680     4   0.270     0.1904 0.000 0.000 0.124 0.876
#&gt; SRR1946681     3   0.758    -0.2242 0.128 0.016 0.472 0.384
#&gt; SRR1946687     3   0.818     0.2878 0.212 0.096 0.568 0.124
#&gt; SRR1946679     2   0.747     0.2198 0.176 0.424 0.400 0.000
#&gt; SRR1946678     1   0.407     0.8080 0.748 0.252 0.000 0.000
#&gt; SRR1946676     2   0.731     0.3951 0.168 0.496 0.336 0.000
#&gt; SRR1946677     2   0.190     0.6500 0.004 0.932 0.064 0.000
#&gt; SRR1946672     3   0.734     0.4264 0.144 0.076 0.652 0.128
#&gt; SRR1946673     2   0.155     0.6554 0.040 0.952 0.008 0.000
#&gt; SRR1946671     2   0.234     0.6413 0.008 0.912 0.080 0.000
#&gt; SRR1946669     2   0.292     0.5467 0.140 0.860 0.000 0.000
#&gt; SRR1946668     2   0.233     0.6070 0.088 0.908 0.004 0.000
#&gt; SRR1946666     1   0.731     0.3195 0.440 0.152 0.408 0.000
#&gt; SRR1946667     4   0.228     0.2103 0.000 0.000 0.096 0.904
#&gt; SRR1946670     4   0.950     0.5738 0.196 0.132 0.308 0.364
#&gt; SRR1946663     2   0.849     0.1944 0.196 0.516 0.068 0.220
#&gt; SRR1946664     4   0.881     0.5503 0.184 0.064 0.352 0.400
#&gt; SRR1946662     2   0.201     0.6186 0.080 0.920 0.000 0.000
#&gt; SRR1946661     2   0.492     0.5656 0.208 0.752 0.036 0.004
#&gt; SRR1946660     4   0.944     0.5814 0.196 0.124 0.308 0.372
#&gt; SRR1946659     1   0.673     0.4652 0.560 0.092 0.344 0.004
#&gt; SRR1946658     3   0.978    -0.5620 0.224 0.168 0.336 0.272
#&gt; SRR1946657     3   0.747    -0.3235 0.176 0.396 0.428 0.000
#&gt; SRR1946655     3   0.454     0.4275 0.000 0.000 0.676 0.324
#&gt; SRR1946654     3   0.655     0.4712 0.088 0.072 0.712 0.128
#&gt; SRR1946653     3   0.783     0.3898 0.160 0.096 0.612 0.132
#&gt; SRR1946652     2   0.718     0.4475 0.184 0.572 0.240 0.004
#&gt; SRR1946651     2   0.751     0.2247 0.184 0.440 0.376 0.000
#&gt; SRR1946650     2   0.622     0.5423 0.188 0.680 0.128 0.004
#&gt; SRR1946649     2   0.254     0.6560 0.012 0.904 0.084 0.000
#&gt; SRR1946648     3   0.719     0.2108 0.064 0.396 0.508 0.032
#&gt; SRR1946647     2   0.259     0.6070 0.080 0.904 0.016 0.000
#&gt; SRR1946646     3   0.572     0.0925 0.152 0.132 0.716 0.000
#&gt; SRR1946645     2   0.274     0.6303 0.024 0.900 0.076 0.000
#&gt; SRR1946644     3   0.880    -0.3269 0.176 0.120 0.512 0.192
#&gt; SRR1946643     3   0.476     0.3983 0.000 0.000 0.628 0.372
#&gt; SRR1946642     1   0.401     0.8111 0.756 0.244 0.000 0.000
#&gt; SRR1946641     1   0.384     0.8239 0.776 0.224 0.000 0.000
#&gt; SRR1946656     3   0.476     0.3983 0.000 0.000 0.628 0.372
#&gt; SRR1946640     1   0.384     0.8239 0.776 0.224 0.000 0.000
#&gt; SRR1946639     1   0.384     0.8239 0.776 0.224 0.000 0.000
#&gt; SRR1946638     1   0.384     0.8239 0.776 0.224 0.000 0.000
#&gt; SRR1946637     1   0.384     0.8239 0.776 0.224 0.000 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3   0.388     0.8005 0.100 0.028 0.828 0.000 0.044
#&gt; SRR1946691     4   0.476     0.3779 0.000 0.288 0.012 0.676 0.024
#&gt; SRR1946690     2   0.483     0.0507 0.000 0.560 0.016 0.420 0.004
#&gt; SRR1946689     4   0.768     0.2800 0.084 0.232 0.148 0.520 0.016
#&gt; SRR1946686     3   0.443     0.7339 0.192 0.000 0.744 0.000 0.064
#&gt; SRR1946685     2   0.511     0.3939 0.000 0.620 0.056 0.000 0.324
#&gt; SRR1946688     4   0.477     0.4018 0.000 0.276 0.004 0.680 0.040
#&gt; SRR1946684     5   0.239     0.7438 0.056 0.004 0.008 0.020 0.912
#&gt; SRR1946683     5   0.460     0.7405 0.004 0.116 0.100 0.008 0.772
#&gt; SRR1946682     4   0.496     0.1892 0.000 0.028 0.000 0.520 0.452
#&gt; SRR1946680     4   0.804     0.2499 0.096 0.260 0.164 0.464 0.016
#&gt; SRR1946681     2   0.702     0.0269 0.012 0.484 0.216 0.280 0.008
#&gt; SRR1946687     3   0.328     0.7996 0.116 0.008 0.848 0.000 0.028
#&gt; SRR1946679     2   0.416     0.5216 0.000 0.704 0.016 0.000 0.280
#&gt; SRR1946678     1   0.233     0.9612 0.876 0.000 0.000 0.000 0.124
#&gt; SRR1946676     2   0.577     0.2093 0.000 0.532 0.096 0.000 0.372
#&gt; SRR1946677     5   0.460     0.7411 0.004 0.116 0.100 0.008 0.772
#&gt; SRR1946672     3   0.301     0.7905 0.056 0.060 0.876 0.000 0.008
#&gt; SRR1946673     5   0.157     0.7624 0.032 0.008 0.012 0.000 0.948
#&gt; SRR1946671     5   0.484     0.7292 0.004 0.120 0.116 0.008 0.752
#&gt; SRR1946669     5   0.212     0.7498 0.076 0.004 0.008 0.000 0.912
#&gt; SRR1946668     5   0.239     0.7496 0.044 0.004 0.016 0.020 0.916
#&gt; SRR1946666     3   0.427     0.7414 0.196 0.000 0.752 0.000 0.052
#&gt; SRR1946667     4   0.768     0.2800 0.084 0.232 0.148 0.520 0.016
#&gt; SRR1946670     4   0.550     0.3902 0.000 0.280 0.004 0.628 0.088
#&gt; SRR1946663     4   0.496     0.1892 0.000 0.028 0.000 0.520 0.452
#&gt; SRR1946664     2   0.483     0.0507 0.000 0.560 0.016 0.420 0.004
#&gt; SRR1946662     5   0.177     0.7580 0.048 0.008 0.008 0.000 0.936
#&gt; SRR1946661     5   0.427     0.6589 0.000 0.104 0.000 0.120 0.776
#&gt; SRR1946660     4   0.477     0.4018 0.000 0.276 0.004 0.680 0.040
#&gt; SRR1946659     3   0.465     0.5931 0.328 0.000 0.644 0.000 0.028
#&gt; SRR1946658     4   0.576     0.3238 0.000 0.332 0.004 0.572 0.092
#&gt; SRR1946657     2   0.411     0.5396 0.000 0.724 0.020 0.000 0.256
#&gt; SRR1946655     3   0.387     0.6976 0.012 0.096 0.832 0.052 0.008
#&gt; SRR1946654     3   0.264     0.7657 0.012 0.088 0.888 0.000 0.012
#&gt; SRR1946653     3   0.342     0.8046 0.096 0.020 0.852 0.000 0.032
#&gt; SRR1946652     5   0.471    -0.0384 0.000 0.492 0.008 0.004 0.496
#&gt; SRR1946651     2   0.411     0.5203 0.000 0.708 0.004 0.008 0.280
#&gt; SRR1946650     5   0.504     0.5107 0.000 0.304 0.008 0.040 0.648
#&gt; SRR1946649     5   0.476     0.6977 0.004 0.188 0.060 0.008 0.740
#&gt; SRR1946648     3   0.483     0.6749 0.020 0.044 0.740 0.004 0.192
#&gt; SRR1946647     5   0.267     0.7487 0.032 0.004 0.040 0.020 0.904
#&gt; SRR1946646     2   0.507     0.4059 0.000 0.640 0.308 0.004 0.048
#&gt; SRR1946645     5   0.502     0.7261 0.012 0.116 0.116 0.008 0.748
#&gt; SRR1946644     2   0.562     0.4044 0.000 0.688 0.144 0.144 0.024
#&gt; SRR1946643     3   0.554     0.5946 0.020 0.184 0.700 0.088 0.008
#&gt; SRR1946642     1   0.228     0.9633 0.880 0.000 0.000 0.000 0.120
#&gt; SRR1946641     1   0.225     0.9852 0.896 0.000 0.008 0.000 0.096
#&gt; SRR1946656     3   0.554     0.5946 0.020 0.184 0.700 0.088 0.008
#&gt; SRR1946640     1   0.225     0.9852 0.896 0.000 0.008 0.000 0.096
#&gt; SRR1946639     1   0.225     0.9852 0.896 0.000 0.008 0.000 0.096
#&gt; SRR1946638     1   0.225     0.9852 0.896 0.000 0.008 0.000 0.096
#&gt; SRR1946637     1   0.225     0.9852 0.896 0.000 0.008 0.000 0.096
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.1605     0.7991 0.032 0.012 0.940 0.000 0.016 0.000
#&gt; SRR1946691     6  0.0881     0.6625 0.008 0.008 0.000 0.012 0.000 0.972
#&gt; SRR1946690     6  0.4519     0.3346 0.008 0.384 0.000 0.024 0.000 0.584
#&gt; SRR1946689     4  0.6503     0.8887 0.016 0.344 0.032 0.496 0.008 0.104
#&gt; SRR1946686     3  0.2039     0.7885 0.076 0.000 0.904 0.000 0.020 0.000
#&gt; SRR1946685     2  0.4897     0.7503 0.000 0.568 0.020 0.000 0.380 0.032
#&gt; SRR1946688     6  0.0405     0.6663 0.000 0.000 0.000 0.008 0.004 0.988
#&gt; SRR1946684     5  0.4377     0.6581 0.016 0.004 0.000 0.296 0.668 0.016
#&gt; SRR1946683     5  0.2099     0.6206 0.004 0.008 0.080 0.000 0.904 0.004
#&gt; SRR1946682     6  0.4980     0.4482 0.000 0.000 0.000 0.168 0.184 0.648
#&gt; SRR1946680     4  0.5192     0.7804 0.000 0.244 0.056 0.652 0.000 0.048
#&gt; SRR1946681     6  0.7430     0.0483 0.004 0.300 0.100 0.264 0.000 0.332
#&gt; SRR1946687     3  0.1152     0.7998 0.044 0.000 0.952 0.000 0.004 0.000
#&gt; SRR1946679     2  0.5248     0.7918 0.000 0.568 0.008 0.000 0.336 0.088
#&gt; SRR1946678     1  0.1398     0.9232 0.940 0.000 0.000 0.008 0.052 0.000
#&gt; SRR1946676     2  0.5105     0.6301 0.000 0.504 0.052 0.000 0.432 0.012
#&gt; SRR1946677     5  0.1988     0.6244 0.004 0.008 0.072 0.000 0.912 0.004
#&gt; SRR1946672     3  0.0748     0.7897 0.004 0.016 0.976 0.000 0.000 0.004
#&gt; SRR1946673     5  0.4159     0.6644 0.016 0.004 0.000 0.288 0.684 0.008
#&gt; SRR1946671     5  0.2257     0.6179 0.008 0.012 0.076 0.000 0.900 0.004
#&gt; SRR1946669     5  0.4074     0.6643 0.024 0.004 0.000 0.288 0.684 0.000
#&gt; SRR1946668     5  0.4377     0.6581 0.016 0.004 0.000 0.296 0.668 0.016
#&gt; SRR1946666     3  0.2039     0.7885 0.076 0.000 0.904 0.000 0.020 0.000
#&gt; SRR1946667     4  0.6503     0.8887 0.016 0.344 0.032 0.496 0.008 0.104
#&gt; SRR1946670     6  0.1275     0.6666 0.000 0.012 0.000 0.016 0.016 0.956
#&gt; SRR1946663     6  0.4980     0.4482 0.000 0.000 0.000 0.168 0.184 0.648
#&gt; SRR1946664     6  0.4519     0.3346 0.008 0.384 0.000 0.024 0.000 0.584
#&gt; SRR1946662     5  0.4134     0.6651 0.020 0.004 0.000 0.288 0.684 0.004
#&gt; SRR1946661     5  0.1333     0.6240 0.000 0.000 0.000 0.008 0.944 0.048
#&gt; SRR1946660     6  0.0405     0.6663 0.000 0.000 0.000 0.008 0.004 0.988
#&gt; SRR1946659     3  0.3309     0.6120 0.280 0.000 0.720 0.000 0.000 0.000
#&gt; SRR1946658     6  0.2345     0.6598 0.000 0.072 0.000 0.016 0.016 0.896
#&gt; SRR1946657     2  0.5347     0.7869 0.000 0.612 0.008 0.008 0.276 0.096
#&gt; SRR1946655     3  0.3921     0.6122 0.000 0.036 0.736 0.224 0.000 0.004
#&gt; SRR1946654     3  0.1010     0.7854 0.000 0.036 0.960 0.000 0.004 0.000
#&gt; SRR1946653     3  0.1296     0.7997 0.032 0.012 0.952 0.004 0.000 0.000
#&gt; SRR1946652     5  0.4531    -0.5887 0.000 0.464 0.000 0.000 0.504 0.032
#&gt; SRR1946651     2  0.5203     0.7938 0.000 0.572 0.004 0.000 0.328 0.096
#&gt; SRR1946650     5  0.3720     0.1918 0.000 0.236 0.000 0.000 0.736 0.028
#&gt; SRR1946649     5  0.2705     0.5651 0.004 0.076 0.040 0.000 0.876 0.004
#&gt; SRR1946648     3  0.2980     0.6854 0.000 0.012 0.808 0.000 0.180 0.000
#&gt; SRR1946647     5  0.4514     0.6578 0.016 0.004 0.004 0.296 0.664 0.016
#&gt; SRR1946646     2  0.5947     0.6336 0.000 0.612 0.192 0.000 0.124 0.072
#&gt; SRR1946645     5  0.2317     0.6136 0.008 0.008 0.088 0.000 0.892 0.004
#&gt; SRR1946644     2  0.5998     0.5316 0.000 0.604 0.068 0.008 0.084 0.236
#&gt; SRR1946643     3  0.5628     0.3676 0.000 0.160 0.540 0.296 0.000 0.004
#&gt; SRR1946642     1  0.0713     0.9535 0.972 0.000 0.000 0.000 0.028 0.000
#&gt; SRR1946641     1  0.1074     0.9785 0.960 0.000 0.028 0.000 0.012 0.000
#&gt; SRR1946656     3  0.5628     0.3676 0.000 0.160 0.540 0.296 0.000 0.004
#&gt; SRR1946640     1  0.1074     0.9785 0.960 0.000 0.028 0.000 0.012 0.000
#&gt; SRR1946639     1  0.1074     0.9785 0.960 0.000 0.028 0.000 0.012 0.000
#&gt; SRR1946638     1  0.1074     0.9785 0.960 0.000 0.028 0.000 0.012 0.000
#&gt; SRR1946637     1  0.1074     0.9785 0.960 0.000 0.028 0.000 0.012 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.847           0.913       0.965         0.5093 0.491   0.491
#> 3 3 0.618           0.773       0.868         0.3232 0.683   0.440
#> 4 4 0.593           0.624       0.782         0.1240 0.819   0.514
#> 5 5 0.673           0.663       0.812         0.0672 0.840   0.454
#> 6 6 0.725           0.646       0.764         0.0400 0.964   0.811
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2   0.996      0.133 0.464 0.536
#&gt; SRR1946691     2   0.000      0.963 0.000 1.000
#&gt; SRR1946690     2   0.000      0.963 0.000 1.000
#&gt; SRR1946689     2   0.000      0.963 0.000 1.000
#&gt; SRR1946686     1   0.000      0.959 1.000 0.000
#&gt; SRR1946685     2   0.000      0.963 0.000 1.000
#&gt; SRR1946688     2   0.000      0.963 0.000 1.000
#&gt; SRR1946684     1   0.000      0.959 1.000 0.000
#&gt; SRR1946683     1   0.000      0.959 1.000 0.000
#&gt; SRR1946682     1   0.827      0.652 0.740 0.260
#&gt; SRR1946680     2   0.000      0.963 0.000 1.000
#&gt; SRR1946681     2   0.000      0.963 0.000 1.000
#&gt; SRR1946687     1   0.506      0.853 0.888 0.112
#&gt; SRR1946679     2   0.000      0.963 0.000 1.000
#&gt; SRR1946678     1   0.000      0.959 1.000 0.000
#&gt; SRR1946676     2   0.000      0.963 0.000 1.000
#&gt; SRR1946677     1   0.000      0.959 1.000 0.000
#&gt; SRR1946672     2   0.722      0.739 0.200 0.800
#&gt; SRR1946673     1   0.000      0.959 1.000 0.000
#&gt; SRR1946671     1   0.000      0.959 1.000 0.000
#&gt; SRR1946669     1   0.000      0.959 1.000 0.000
#&gt; SRR1946668     1   0.000      0.959 1.000 0.000
#&gt; SRR1946666     1   0.000      0.959 1.000 0.000
#&gt; SRR1946667     2   0.000      0.963 0.000 1.000
#&gt; SRR1946670     2   0.000      0.963 0.000 1.000
#&gt; SRR1946663     1   0.141      0.943 0.980 0.020
#&gt; SRR1946664     2   0.000      0.963 0.000 1.000
#&gt; SRR1946662     1   0.000      0.959 1.000 0.000
#&gt; SRR1946661     1   0.000      0.959 1.000 0.000
#&gt; SRR1946660     2   0.000      0.963 0.000 1.000
#&gt; SRR1946659     1   0.000      0.959 1.000 0.000
#&gt; SRR1946658     2   0.000      0.963 0.000 1.000
#&gt; SRR1946657     2   0.000      0.963 0.000 1.000
#&gt; SRR1946655     2   0.000      0.963 0.000 1.000
#&gt; SRR1946654     2   0.000      0.963 0.000 1.000
#&gt; SRR1946653     2   0.745      0.721 0.212 0.788
#&gt; SRR1946652     2   0.000      0.963 0.000 1.000
#&gt; SRR1946651     2   0.000      0.963 0.000 1.000
#&gt; SRR1946650     1   0.921      0.511 0.664 0.336
#&gt; SRR1946649     1   0.000      0.959 1.000 0.000
#&gt; SRR1946648     1   0.839      0.621 0.732 0.268
#&gt; SRR1946647     1   0.000      0.959 1.000 0.000
#&gt; SRR1946646     2   0.000      0.963 0.000 1.000
#&gt; SRR1946645     1   0.000      0.959 1.000 0.000
#&gt; SRR1946644     2   0.000      0.963 0.000 1.000
#&gt; SRR1946643     2   0.000      0.963 0.000 1.000
#&gt; SRR1946642     1   0.000      0.959 1.000 0.000
#&gt; SRR1946641     1   0.000      0.959 1.000 0.000
#&gt; SRR1946656     2   0.000      0.963 0.000 1.000
#&gt; SRR1946640     1   0.000      0.959 1.000 0.000
#&gt; SRR1946639     1   0.000      0.959 1.000 0.000
#&gt; SRR1946638     1   0.000      0.959 1.000 0.000
#&gt; SRR1946637     1   0.000      0.959 1.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.0592      0.773 0.012 0.000 0.988
#&gt; SRR1946691     2  0.0000      0.870 0.000 1.000 0.000
#&gt; SRR1946690     2  0.0000      0.870 0.000 1.000 0.000
#&gt; SRR1946689     3  0.5591      0.691 0.000 0.304 0.696
#&gt; SRR1946686     1  0.6308      0.349 0.508 0.000 0.492
#&gt; SRR1946685     2  0.2280      0.850 0.008 0.940 0.052
#&gt; SRR1946688     2  0.0592      0.872 0.012 0.988 0.000
#&gt; SRR1946684     1  0.0000      0.868 1.000 0.000 0.000
#&gt; SRR1946683     1  0.0424      0.870 0.992 0.000 0.008
#&gt; SRR1946682     2  0.4452      0.775 0.192 0.808 0.000
#&gt; SRR1946680     3  0.5560      0.695 0.000 0.300 0.700
#&gt; SRR1946681     2  0.2448      0.825 0.000 0.924 0.076
#&gt; SRR1946687     3  0.0747      0.771 0.016 0.000 0.984
#&gt; SRR1946679     2  0.1170      0.869 0.008 0.976 0.016
#&gt; SRR1946678     1  0.4291      0.864 0.820 0.000 0.180
#&gt; SRR1946676     2  0.3607      0.797 0.008 0.880 0.112
#&gt; SRR1946677     1  0.0000      0.868 1.000 0.000 0.000
#&gt; SRR1946672     3  0.0000      0.777 0.000 0.000 1.000
#&gt; SRR1946673     1  0.0892      0.853 0.980 0.020 0.000
#&gt; SRR1946671     1  0.3879      0.870 0.848 0.000 0.152
#&gt; SRR1946669     1  0.0000      0.868 1.000 0.000 0.000
#&gt; SRR1946668     1  0.0424      0.870 0.992 0.000 0.008
#&gt; SRR1946666     3  0.6267     -0.266 0.452 0.000 0.548
#&gt; SRR1946667     3  0.5591      0.691 0.000 0.304 0.696
#&gt; SRR1946670     2  0.0747      0.872 0.016 0.984 0.000
#&gt; SRR1946663     2  0.4931      0.742 0.232 0.768 0.000
#&gt; SRR1946664     2  0.0000      0.870 0.000 1.000 0.000
#&gt; SRR1946662     1  0.0000      0.868 1.000 0.000 0.000
#&gt; SRR1946661     2  0.5968      0.569 0.364 0.636 0.000
#&gt; SRR1946660     2  0.0592      0.872 0.012 0.988 0.000
#&gt; SRR1946659     3  0.1964      0.737 0.056 0.000 0.944
#&gt; SRR1946658     2  0.0747      0.872 0.016 0.984 0.000
#&gt; SRR1946657     2  0.0983      0.868 0.004 0.980 0.016
#&gt; SRR1946655     3  0.4452      0.761 0.000 0.192 0.808
#&gt; SRR1946654     3  0.2066      0.789 0.000 0.060 0.940
#&gt; SRR1946653     3  0.0592      0.773 0.012 0.000 0.988
#&gt; SRR1946652     2  0.4808      0.778 0.188 0.804 0.008
#&gt; SRR1946651     2  0.1015      0.870 0.008 0.980 0.012
#&gt; SRR1946650     2  0.4504      0.772 0.196 0.804 0.000
#&gt; SRR1946649     1  0.0475      0.868 0.992 0.004 0.004
#&gt; SRR1946648     3  0.4121      0.724 0.168 0.000 0.832
#&gt; SRR1946647     1  0.0237      0.869 0.996 0.000 0.004
#&gt; SRR1946646     3  0.5968      0.562 0.000 0.364 0.636
#&gt; SRR1946645     1  0.3941      0.870 0.844 0.000 0.156
#&gt; SRR1946644     2  0.5926      0.224 0.000 0.644 0.356
#&gt; SRR1946643     3  0.4452      0.761 0.000 0.192 0.808
#&gt; SRR1946642     1  0.4291      0.864 0.820 0.000 0.180
#&gt; SRR1946641     1  0.4452      0.859 0.808 0.000 0.192
#&gt; SRR1946656     3  0.4452      0.761 0.000 0.192 0.808
#&gt; SRR1946640     1  0.4452      0.859 0.808 0.000 0.192
#&gt; SRR1946639     1  0.4452      0.859 0.808 0.000 0.192
#&gt; SRR1946638     1  0.4452      0.859 0.808 0.000 0.192
#&gt; SRR1946637     1  0.4452      0.859 0.808 0.000 0.192
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.3172     0.7760 0.160 0.000 0.840 0.000
#&gt; SRR1946691     4  0.0188     0.8332 0.000 0.004 0.000 0.996
#&gt; SRR1946690     4  0.3081     0.7900 0.000 0.064 0.048 0.888
#&gt; SRR1946689     4  0.3539     0.7590 0.000 0.004 0.176 0.820
#&gt; SRR1946686     1  0.4776    -0.0198 0.624 0.000 0.376 0.000
#&gt; SRR1946685     2  0.5951     0.5996 0.000 0.696 0.152 0.152
#&gt; SRR1946688     4  0.0188     0.8332 0.000 0.004 0.000 0.996
#&gt; SRR1946684     1  0.4946     0.6243 0.680 0.308 0.008 0.004
#&gt; SRR1946683     1  0.4769     0.5815 0.684 0.308 0.008 0.000
#&gt; SRR1946682     4  0.4020     0.7343 0.016 0.156 0.008 0.820
#&gt; SRR1946680     4  0.4053     0.7190 0.000 0.004 0.228 0.768
#&gt; SRR1946681     4  0.5968     0.6174 0.000 0.092 0.236 0.672
#&gt; SRR1946687     3  0.3311     0.7693 0.172 0.000 0.828 0.000
#&gt; SRR1946679     2  0.5906     0.6005 0.000 0.700 0.152 0.148
#&gt; SRR1946678     1  0.1109     0.7326 0.968 0.028 0.004 0.000
#&gt; SRR1946676     2  0.5812     0.6074 0.000 0.708 0.156 0.136
#&gt; SRR1946677     2  0.4814     0.2596 0.316 0.676 0.008 0.000
#&gt; SRR1946672     3  0.1474     0.7908 0.052 0.000 0.948 0.000
#&gt; SRR1946673     2  0.5112     0.1631 0.340 0.648 0.008 0.004
#&gt; SRR1946671     2  0.4991     0.1489 0.388 0.608 0.004 0.000
#&gt; SRR1946669     1  0.4746     0.6275 0.688 0.304 0.008 0.000
#&gt; SRR1946668     1  0.4799     0.6450 0.704 0.284 0.008 0.004
#&gt; SRR1946666     3  0.4907     0.4901 0.420 0.000 0.580 0.000
#&gt; SRR1946667     4  0.3583     0.7565 0.000 0.004 0.180 0.816
#&gt; SRR1946670     4  0.0817     0.8301 0.000 0.024 0.000 0.976
#&gt; SRR1946663     4  0.4020     0.7343 0.016 0.156 0.008 0.820
#&gt; SRR1946664     4  0.3071     0.7892 0.000 0.068 0.044 0.888
#&gt; SRR1946662     1  0.5070     0.5398 0.620 0.372 0.008 0.000
#&gt; SRR1946661     2  0.5083     0.3874 0.220 0.740 0.008 0.032
#&gt; SRR1946660     4  0.0188     0.8332 0.000 0.004 0.000 0.996
#&gt; SRR1946659     3  0.4776     0.5648 0.376 0.000 0.624 0.000
#&gt; SRR1946658     4  0.0707     0.8313 0.000 0.020 0.000 0.980
#&gt; SRR1946657     2  0.5994     0.5957 0.000 0.692 0.152 0.156
#&gt; SRR1946655     3  0.1256     0.7725 0.000 0.008 0.964 0.028
#&gt; SRR1946654     3  0.0524     0.7789 0.000 0.008 0.988 0.004
#&gt; SRR1946653     3  0.3172     0.7760 0.160 0.000 0.840 0.000
#&gt; SRR1946652     2  0.3498     0.6206 0.000 0.832 0.008 0.160
#&gt; SRR1946651     2  0.5770     0.6063 0.000 0.712 0.140 0.148
#&gt; SRR1946650     2  0.2197     0.6058 0.004 0.916 0.000 0.080
#&gt; SRR1946649     2  0.4406     0.3279 0.300 0.700 0.000 0.000
#&gt; SRR1946648     3  0.4710     0.6973 0.088 0.120 0.792 0.000
#&gt; SRR1946647     1  0.4799     0.6450 0.704 0.284 0.008 0.004
#&gt; SRR1946646     3  0.7166     0.1959 0.000 0.280 0.544 0.176
#&gt; SRR1946645     1  0.5132     0.1010 0.548 0.448 0.004 0.000
#&gt; SRR1946644     4  0.6818     0.4810 0.000 0.232 0.168 0.600
#&gt; SRR1946643     3  0.1820     0.7629 0.000 0.020 0.944 0.036
#&gt; SRR1946642     1  0.1004     0.7330 0.972 0.024 0.004 0.000
#&gt; SRR1946641     1  0.0817     0.7309 0.976 0.000 0.024 0.000
#&gt; SRR1946656     3  0.1724     0.7656 0.000 0.020 0.948 0.032
#&gt; SRR1946640     1  0.0817     0.7309 0.976 0.000 0.024 0.000
#&gt; SRR1946639     1  0.0817     0.7309 0.976 0.000 0.024 0.000
#&gt; SRR1946638     1  0.0817     0.7309 0.976 0.000 0.024 0.000
#&gt; SRR1946637     1  0.0817     0.7309 0.976 0.000 0.024 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.2237      0.777 0.084 0.004 0.904 0.000 0.008
#&gt; SRR1946691     4  0.0000      0.784 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946690     4  0.4776      0.496 0.000 0.296 0.008 0.668 0.028
#&gt; SRR1946689     4  0.4274      0.691 0.000 0.020 0.172 0.776 0.032
#&gt; SRR1946686     1  0.4064      0.613 0.716 0.004 0.272 0.000 0.008
#&gt; SRR1946685     2  0.1815      0.802 0.000 0.940 0.016 0.024 0.020
#&gt; SRR1946688     4  0.0404      0.785 0.000 0.000 0.000 0.988 0.012
#&gt; SRR1946684     5  0.3003      0.690 0.188 0.000 0.000 0.000 0.812
#&gt; SRR1946683     5  0.6461      0.467 0.356 0.136 0.012 0.000 0.496
#&gt; SRR1946682     4  0.3452      0.638 0.000 0.000 0.000 0.756 0.244
#&gt; SRR1946680     4  0.5217      0.497 0.000 0.020 0.312 0.636 0.032
#&gt; SRR1946681     3  0.6977     -0.105 0.000 0.148 0.432 0.388 0.032
#&gt; SRR1946687     3  0.3439      0.674 0.188 0.004 0.800 0.000 0.008
#&gt; SRR1946679     2  0.2116      0.803 0.000 0.924 0.008 0.040 0.028
#&gt; SRR1946678     1  0.1270      0.780 0.948 0.000 0.000 0.000 0.052
#&gt; SRR1946676     2  0.2349      0.763 0.000 0.900 0.012 0.004 0.084
#&gt; SRR1946677     5  0.5149      0.581 0.060 0.232 0.016 0.000 0.692
#&gt; SRR1946672     3  0.0609      0.804 0.020 0.000 0.980 0.000 0.000
#&gt; SRR1946673     5  0.2889      0.695 0.084 0.044 0.000 0.000 0.872
#&gt; SRR1946671     5  0.6311      0.537 0.152 0.252 0.016 0.000 0.580
#&gt; SRR1946669     5  0.3210      0.686 0.212 0.000 0.000 0.000 0.788
#&gt; SRR1946668     5  0.3177      0.678 0.208 0.000 0.000 0.000 0.792
#&gt; SRR1946666     1  0.4613      0.359 0.580 0.004 0.408 0.000 0.008
#&gt; SRR1946667     4  0.4312      0.687 0.000 0.020 0.176 0.772 0.032
#&gt; SRR1946670     4  0.0880      0.782 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1946663     4  0.3480      0.634 0.000 0.000 0.000 0.752 0.248
#&gt; SRR1946664     4  0.4735      0.485 0.000 0.304 0.008 0.664 0.024
#&gt; SRR1946662     5  0.3280      0.699 0.176 0.012 0.000 0.000 0.812
#&gt; SRR1946661     5  0.4029      0.616 0.004 0.116 0.008 0.060 0.812
#&gt; SRR1946660     4  0.0404      0.785 0.000 0.000 0.000 0.988 0.012
#&gt; SRR1946659     1  0.4317      0.531 0.668 0.004 0.320 0.000 0.008
#&gt; SRR1946658     4  0.1741      0.770 0.000 0.040 0.000 0.936 0.024
#&gt; SRR1946657     2  0.2433      0.790 0.000 0.908 0.024 0.056 0.012
#&gt; SRR1946655     3  0.0798      0.806 0.000 0.016 0.976 0.000 0.008
#&gt; SRR1946654     3  0.0404      0.807 0.000 0.012 0.988 0.000 0.000
#&gt; SRR1946653     3  0.2660      0.748 0.128 0.000 0.864 0.000 0.008
#&gt; SRR1946652     2  0.2856      0.742 0.000 0.872 0.008 0.016 0.104
#&gt; SRR1946651     2  0.2267      0.803 0.000 0.916 0.008 0.048 0.028
#&gt; SRR1946650     2  0.4839      0.428 0.000 0.672 0.012 0.028 0.288
#&gt; SRR1946649     5  0.6478      0.416 0.144 0.336 0.012 0.000 0.508
#&gt; SRR1946648     3  0.4853      0.643 0.060 0.024 0.744 0.000 0.172
#&gt; SRR1946647     5  0.3231      0.681 0.196 0.000 0.000 0.004 0.800
#&gt; SRR1946646     2  0.5666      0.569 0.000 0.680 0.188 0.104 0.028
#&gt; SRR1946645     5  0.6918      0.372 0.360 0.192 0.016 0.000 0.432
#&gt; SRR1946644     2  0.5964      0.380 0.000 0.604 0.076 0.292 0.028
#&gt; SRR1946643     3  0.3488      0.754 0.000 0.072 0.856 0.040 0.032
#&gt; SRR1946642     1  0.0963      0.800 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1946641     1  0.0162      0.828 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946656     3  0.3411      0.757 0.000 0.072 0.860 0.036 0.032
#&gt; SRR1946640     1  0.0162      0.828 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946639     1  0.0162      0.828 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946638     1  0.0162      0.828 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946637     1  0.0162      0.828 0.996 0.000 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.2826      0.692 0.052 0.000 0.876 0.056 0.012 0.004
#&gt; SRR1946691     6  0.1148      0.692 0.000 0.016 0.000 0.020 0.004 0.960
#&gt; SRR1946690     6  0.6897      0.269 0.000 0.320 0.016 0.144 0.060 0.460
#&gt; SRR1946689     6  0.6863      0.476 0.000 0.032 0.148 0.196 0.072 0.552
#&gt; SRR1946686     1  0.5176      0.417 0.564 0.000 0.364 0.056 0.012 0.004
#&gt; SRR1946685     2  0.1555      0.754 0.000 0.932 0.004 0.060 0.000 0.004
#&gt; SRR1946688     6  0.0260      0.693 0.000 0.008 0.000 0.000 0.000 0.992
#&gt; SRR1946684     5  0.2135      0.952 0.128 0.000 0.000 0.000 0.872 0.000
#&gt; SRR1946683     4  0.5388      0.685 0.192 0.004 0.000 0.604 0.200 0.000
#&gt; SRR1946682     6  0.3284      0.563 0.000 0.000 0.000 0.020 0.196 0.784
#&gt; SRR1946680     6  0.7595      0.132 0.000 0.032 0.316 0.192 0.080 0.380
#&gt; SRR1946681     3  0.8013      0.173 0.000 0.116 0.440 0.168 0.084 0.192
#&gt; SRR1946687     3  0.5063      0.519 0.168 0.004 0.700 0.104 0.020 0.004
#&gt; SRR1946679     2  0.1245      0.763 0.000 0.952 0.000 0.032 0.000 0.016
#&gt; SRR1946678     1  0.1007      0.787 0.956 0.000 0.000 0.000 0.044 0.000
#&gt; SRR1946676     2  0.3383      0.524 0.000 0.728 0.000 0.268 0.004 0.000
#&gt; SRR1946677     4  0.4714      0.763 0.032 0.052 0.000 0.700 0.216 0.000
#&gt; SRR1946672     3  0.1138      0.727 0.024 0.000 0.960 0.012 0.004 0.000
#&gt; SRR1946673     5  0.2714      0.878 0.060 0.004 0.000 0.064 0.872 0.000
#&gt; SRR1946671     4  0.5561      0.779 0.072 0.088 0.000 0.652 0.188 0.000
#&gt; SRR1946669     5  0.2442      0.944 0.144 0.000 0.000 0.004 0.852 0.000
#&gt; SRR1946668     5  0.2340      0.937 0.148 0.000 0.000 0.000 0.852 0.000
#&gt; SRR1946666     1  0.5579      0.257 0.484 0.000 0.420 0.076 0.016 0.004
#&gt; SRR1946667     6  0.6863      0.476 0.000 0.032 0.148 0.196 0.072 0.552
#&gt; SRR1946670     6  0.0717      0.691 0.000 0.008 0.000 0.000 0.016 0.976
#&gt; SRR1946663     6  0.3345      0.554 0.000 0.000 0.000 0.020 0.204 0.776
#&gt; SRR1946664     6  0.6836      0.198 0.000 0.356 0.016 0.140 0.052 0.436
#&gt; SRR1946662     5  0.2398      0.939 0.104 0.000 0.000 0.020 0.876 0.000
#&gt; SRR1946661     4  0.5233      0.457 0.000 0.032 0.000 0.508 0.424 0.036
#&gt; SRR1946660     6  0.0405      0.693 0.000 0.008 0.000 0.000 0.004 0.988
#&gt; SRR1946659     1  0.5006      0.535 0.648 0.000 0.272 0.056 0.020 0.004
#&gt; SRR1946658     6  0.1528      0.679 0.000 0.048 0.000 0.000 0.016 0.936
#&gt; SRR1946657     2  0.1605      0.747 0.000 0.940 0.000 0.032 0.012 0.016
#&gt; SRR1946655     3  0.2138      0.716 0.000 0.000 0.908 0.052 0.036 0.004
#&gt; SRR1946654     3  0.0291      0.734 0.000 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1946653     3  0.3583      0.681 0.068 0.004 0.832 0.076 0.016 0.004
#&gt; SRR1946652     2  0.3859      0.587 0.000 0.756 0.000 0.204 0.016 0.024
#&gt; SRR1946651     2  0.1074      0.763 0.000 0.960 0.000 0.028 0.000 0.012
#&gt; SRR1946650     4  0.5838      0.485 0.000 0.308 0.000 0.556 0.092 0.044
#&gt; SRR1946649     4  0.5410      0.772 0.072 0.120 0.000 0.680 0.128 0.000
#&gt; SRR1946648     3  0.5283      0.508 0.024 0.000 0.640 0.252 0.080 0.004
#&gt; SRR1946647     5  0.2346      0.951 0.124 0.000 0.000 0.008 0.868 0.000
#&gt; SRR1946646     2  0.5632      0.575 0.000 0.688 0.120 0.116 0.044 0.032
#&gt; SRR1946645     4  0.4969      0.731 0.192 0.020 0.000 0.684 0.104 0.000
#&gt; SRR1946644     2  0.6746      0.375 0.000 0.584 0.056 0.164 0.056 0.140
#&gt; SRR1946643     3  0.5516      0.567 0.000 0.040 0.680 0.176 0.080 0.024
#&gt; SRR1946642     1  0.0713      0.801 0.972 0.000 0.000 0.000 0.028 0.000
#&gt; SRR1946641     1  0.0000      0.820 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.5439      0.572 0.000 0.040 0.684 0.176 0.080 0.020
#&gt; SRR1946640     1  0.0000      0.820 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.820 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.820 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.820 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.418           0.692       0.876         0.4366 0.586   0.586
#> 3 3 0.412           0.590       0.797         0.4649 0.692   0.500
#> 4 4 0.569           0.752       0.849         0.0948 0.906   0.744
#> 5 5 0.798           0.787       0.901         0.1104 0.808   0.461
#> 6 6 0.768           0.738       0.886         0.0481 0.959   0.813
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.9323     0.4727 0.348 0.652
#&gt; SRR1946691     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946690     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946689     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946686     2  0.9393     0.4581 0.356 0.644
#&gt; SRR1946685     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946688     2  0.0938     0.8376 0.012 0.988
#&gt; SRR1946684     1  0.6048     0.7080 0.852 0.148
#&gt; SRR1946683     2  0.9977     0.2182 0.472 0.528
#&gt; SRR1946682     2  0.5294     0.7573 0.120 0.880
#&gt; SRR1946680     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946681     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946687     2  0.9323     0.4727 0.348 0.652
#&gt; SRR1946679     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946678     1  0.0000     0.8095 1.000 0.000
#&gt; SRR1946676     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946677     2  0.6973     0.6921 0.188 0.812
#&gt; SRR1946672     2  0.8608     0.5725 0.284 0.716
#&gt; SRR1946673     2  0.6801     0.7016 0.180 0.820
#&gt; SRR1946671     2  0.7883     0.6747 0.236 0.764
#&gt; SRR1946669     1  0.0000     0.8095 1.000 0.000
#&gt; SRR1946668     1  0.9866     0.0339 0.568 0.432
#&gt; SRR1946666     2  0.9552     0.4184 0.376 0.624
#&gt; SRR1946667     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946670     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946663     2  0.9866     0.3076 0.432 0.568
#&gt; SRR1946664     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946662     1  0.8443     0.5534 0.728 0.272
#&gt; SRR1946661     2  0.8144     0.5965 0.252 0.748
#&gt; SRR1946660     2  0.2778     0.8149 0.048 0.952
#&gt; SRR1946659     1  0.4815     0.7352 0.896 0.104
#&gt; SRR1946658     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946657     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946655     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946654     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946653     2  0.9323     0.4727 0.348 0.652
#&gt; SRR1946652     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946651     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946650     2  0.6712     0.7005 0.176 0.824
#&gt; SRR1946649     1  0.9754     0.3183 0.592 0.408
#&gt; SRR1946648     2  0.9286     0.4794 0.344 0.656
#&gt; SRR1946647     1  0.9988    -0.1327 0.520 0.480
#&gt; SRR1946646     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946645     1  0.7376     0.6115 0.792 0.208
#&gt; SRR1946644     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946643     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946642     1  0.0000     0.8095 1.000 0.000
#&gt; SRR1946641     1  0.0000     0.8095 1.000 0.000
#&gt; SRR1946656     2  0.0000     0.8439 0.000 1.000
#&gt; SRR1946640     1  0.0000     0.8095 1.000 0.000
#&gt; SRR1946639     1  0.0000     0.8095 1.000 0.000
#&gt; SRR1946638     1  0.0000     0.8095 1.000 0.000
#&gt; SRR1946637     1  0.0000     0.8095 1.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.4137    0.72929 0.096 0.032 0.872
#&gt; SRR1946691     2  0.0237    0.68972 0.000 0.996 0.004
#&gt; SRR1946690     2  0.1529    0.67397 0.000 0.960 0.040
#&gt; SRR1946689     3  0.6235    0.00653 0.000 0.436 0.564
#&gt; SRR1946686     3  0.4062    0.70950 0.164 0.000 0.836
#&gt; SRR1946685     3  0.6140    0.24113 0.000 0.404 0.596
#&gt; SRR1946688     2  0.0000    0.69088 0.000 1.000 0.000
#&gt; SRR1946684     1  0.3038    0.82072 0.896 0.104 0.000
#&gt; SRR1946683     3  0.6247    0.66184 0.212 0.044 0.744
#&gt; SRR1946682     2  0.0000    0.69088 0.000 1.000 0.000
#&gt; SRR1946680     3  0.0000    0.69685 0.000 0.000 1.000
#&gt; SRR1946681     3  0.5810    0.36083 0.000 0.336 0.664
#&gt; SRR1946687     3  0.3845    0.72699 0.116 0.012 0.872
#&gt; SRR1946679     2  0.6235    0.22731 0.000 0.564 0.436
#&gt; SRR1946678     1  0.0000    0.89711 1.000 0.000 0.000
#&gt; SRR1946676     3  0.4178    0.67135 0.000 0.172 0.828
#&gt; SRR1946677     3  0.7712    0.19958 0.052 0.392 0.556
#&gt; SRR1946672     3  0.3129    0.72721 0.088 0.008 0.904
#&gt; SRR1946673     2  0.8668    0.30746 0.132 0.564 0.304
#&gt; SRR1946671     3  0.6811    0.59690 0.064 0.220 0.716
#&gt; SRR1946669     1  0.1529    0.87391 0.960 0.040 0.000
#&gt; SRR1946668     3  0.7578    0.25892 0.460 0.040 0.500
#&gt; SRR1946666     3  0.5178    0.64131 0.256 0.000 0.744
#&gt; SRR1946667     3  0.6235    0.00653 0.000 0.436 0.564
#&gt; SRR1946670     2  0.6225    0.02283 0.000 0.568 0.432
#&gt; SRR1946663     2  0.8891    0.08173 0.340 0.524 0.136
#&gt; SRR1946664     2  0.1411    0.67487 0.000 0.964 0.036
#&gt; SRR1946662     1  0.4750    0.68475 0.784 0.216 0.000
#&gt; SRR1946661     2  0.3879    0.61710 0.000 0.848 0.152
#&gt; SRR1946660     2  0.0000    0.69088 0.000 1.000 0.000
#&gt; SRR1946659     1  0.0000    0.89711 1.000 0.000 0.000
#&gt; SRR1946658     2  0.0000    0.69088 0.000 1.000 0.000
#&gt; SRR1946657     2  0.6267    0.21403 0.000 0.548 0.452
#&gt; SRR1946655     3  0.2878    0.70952 0.000 0.096 0.904
#&gt; SRR1946654     3  0.3412    0.70563 0.000 0.124 0.876
#&gt; SRR1946653     3  0.3644    0.72432 0.124 0.004 0.872
#&gt; SRR1946652     2  0.6244    0.22157 0.000 0.560 0.440
#&gt; SRR1946651     2  0.4750    0.56836 0.000 0.784 0.216
#&gt; SRR1946650     2  0.0000    0.69088 0.000 1.000 0.000
#&gt; SRR1946649     1  0.8688    0.42276 0.596 0.208 0.196
#&gt; SRR1946648     3  0.4137    0.72929 0.096 0.032 0.872
#&gt; SRR1946647     3  0.6867    0.59460 0.288 0.040 0.672
#&gt; SRR1946646     3  0.3267    0.70808 0.000 0.116 0.884
#&gt; SRR1946645     1  0.6379    0.51041 0.712 0.032 0.256
#&gt; SRR1946644     2  0.6299    0.19753 0.000 0.524 0.476
#&gt; SRR1946643     3  0.2878    0.70952 0.000 0.096 0.904
#&gt; SRR1946642     1  0.0000    0.89711 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000    0.89711 1.000 0.000 0.000
#&gt; SRR1946656     3  0.2878    0.70952 0.000 0.096 0.904
#&gt; SRR1946640     1  0.0000    0.89711 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000    0.89711 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000    0.89711 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000    0.89711 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1946675     3  0.0000      0.744 0.000 0.000 1.000  0
#&gt; SRR1946691     2  0.0000      0.907 0.000 1.000 0.000  0
#&gt; SRR1946690     2  0.0592      0.906 0.000 0.984 0.016  0
#&gt; SRR1946689     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1946686     3  0.3123      0.721 0.156 0.000 0.844  0
#&gt; SRR1946685     3  0.4996      0.298 0.000 0.484 0.516  0
#&gt; SRR1946688     2  0.1022      0.906 0.000 0.968 0.032  0
#&gt; SRR1946684     1  0.3597      0.761 0.836 0.016 0.148  0
#&gt; SRR1946683     3  0.3768      0.641 0.184 0.008 0.808  0
#&gt; SRR1946682     2  0.3024      0.817 0.000 0.852 0.148  0
#&gt; SRR1946680     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1946681     3  0.4961      0.391 0.000 0.448 0.552  0
#&gt; SRR1946687     3  0.0817      0.747 0.024 0.000 0.976  0
#&gt; SRR1946679     2  0.1637      0.897 0.000 0.940 0.060  0
#&gt; SRR1946678     1  0.0000      0.860 1.000 0.000 0.000  0
#&gt; SRR1946676     3  0.4008      0.694 0.000 0.244 0.756  0
#&gt; SRR1946677     3  0.6206      0.171 0.056 0.404 0.540  0
#&gt; SRR1946672     3  0.3249      0.727 0.140 0.008 0.852  0
#&gt; SRR1946673     2  0.4114      0.819 0.060 0.828 0.112  0
#&gt; SRR1946671     3  0.5631      0.600 0.072 0.232 0.696  0
#&gt; SRR1946669     1  0.3597      0.761 0.836 0.016 0.148  0
#&gt; SRR1946668     3  0.5203      0.372 0.348 0.016 0.636  0
#&gt; SRR1946666     3  0.3610      0.695 0.200 0.000 0.800  0
#&gt; SRR1946667     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1946670     3  0.1940      0.717 0.000 0.076 0.924  0
#&gt; SRR1946663     3  0.6510      0.191 0.380 0.080 0.540  0
#&gt; SRR1946664     2  0.0592      0.906 0.000 0.984 0.016  0
#&gt; SRR1946662     1  0.5906      0.638 0.700 0.152 0.148  0
#&gt; SRR1946661     2  0.2469      0.860 0.000 0.892 0.108  0
#&gt; SRR1946660     2  0.0817      0.907 0.000 0.976 0.024  0
#&gt; SRR1946659     1  0.0000      0.860 1.000 0.000 0.000  0
#&gt; SRR1946658     2  0.2647      0.842 0.000 0.880 0.120  0
#&gt; SRR1946657     2  0.1940      0.886 0.000 0.924 0.076  0
#&gt; SRR1946655     3  0.3024      0.745 0.000 0.148 0.852  0
#&gt; SRR1946654     3  0.2647      0.750 0.000 0.120 0.880  0
#&gt; SRR1946653     3  0.2921      0.728 0.140 0.000 0.860  0
#&gt; SRR1946652     2  0.2408      0.886 0.000 0.896 0.104  0
#&gt; SRR1946651     2  0.1474      0.901 0.000 0.948 0.052  0
#&gt; SRR1946650     2  0.0336      0.909 0.000 0.992 0.008  0
#&gt; SRR1946649     1  0.6445      0.436 0.600 0.304 0.096  0
#&gt; SRR1946648     3  0.0000      0.744 0.000 0.000 1.000  0
#&gt; SRR1946647     3  0.3108      0.703 0.112 0.016 0.872  0
#&gt; SRR1946646     3  0.3024      0.745 0.000 0.148 0.852  0
#&gt; SRR1946645     1  0.4193      0.552 0.732 0.000 0.268  0
#&gt; SRR1946644     2  0.1940      0.886 0.000 0.924 0.076  0
#&gt; SRR1946643     3  0.3024      0.745 0.000 0.148 0.852  0
#&gt; SRR1946642     1  0.0000      0.860 1.000 0.000 0.000  0
#&gt; SRR1946641     1  0.0000      0.860 1.000 0.000 0.000  0
#&gt; SRR1946656     3  0.3024      0.745 0.000 0.148 0.852  0
#&gt; SRR1946640     1  0.0000      0.860 1.000 0.000 0.000  0
#&gt; SRR1946639     1  0.0000      0.860 1.000 0.000 0.000  0
#&gt; SRR1946638     1  0.0000      0.860 1.000 0.000 0.000  0
#&gt; SRR1946637     1  0.0000      0.860 1.000 0.000 0.000  0
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.0703     0.8526 0.000 0.000 0.976 0.000 0.024
#&gt; SRR1946691     2  0.2891     0.7546 0.000 0.824 0.000 0.000 0.176
#&gt; SRR1946690     2  0.0290     0.8857 0.000 0.992 0.008 0.000 0.000
#&gt; SRR1946689     4  0.0000     0.9983 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946686     3  0.1043     0.8533 0.040 0.000 0.960 0.000 0.000
#&gt; SRR1946685     2  0.4291    -0.0304 0.000 0.536 0.464 0.000 0.000
#&gt; SRR1946688     5  0.4287     0.0913 0.000 0.460 0.000 0.000 0.540
#&gt; SRR1946684     5  0.2654     0.8547 0.040 0.044 0.016 0.000 0.900
#&gt; SRR1946683     5  0.3861     0.6175 0.008 0.000 0.264 0.000 0.728
#&gt; SRR1946682     5  0.0290     0.8500 0.000 0.008 0.000 0.000 0.992
#&gt; SRR1946680     4  0.0162     0.9966 0.000 0.000 0.004 0.996 0.000
#&gt; SRR1946681     3  0.4291     0.1321 0.000 0.464 0.536 0.000 0.000
#&gt; SRR1946687     3  0.1648     0.8490 0.020 0.000 0.940 0.000 0.040
#&gt; SRR1946679     2  0.0609     0.8866 0.000 0.980 0.020 0.000 0.000
#&gt; SRR1946678     1  0.0000     0.9026 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     3  0.4219     0.6049 0.000 0.260 0.716 0.000 0.024
#&gt; SRR1946677     5  0.2423     0.8437 0.000 0.024 0.080 0.000 0.896
#&gt; SRR1946672     3  0.0703     0.8559 0.024 0.000 0.976 0.000 0.000
#&gt; SRR1946673     5  0.2411     0.8358 0.000 0.108 0.008 0.000 0.884
#&gt; SRR1946671     3  0.6832     0.3614 0.072 0.088 0.536 0.000 0.304
#&gt; SRR1946669     5  0.2873     0.8098 0.128 0.000 0.016 0.000 0.856
#&gt; SRR1946668     5  0.2450     0.8499 0.052 0.000 0.048 0.000 0.900
#&gt; SRR1946666     3  0.1671     0.8304 0.076 0.000 0.924 0.000 0.000
#&gt; SRR1946667     4  0.0000     0.9983 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946670     5  0.1117     0.8486 0.000 0.020 0.016 0.000 0.964
#&gt; SRR1946663     5  0.0290     0.8500 0.000 0.008 0.000 0.000 0.992
#&gt; SRR1946664     2  0.0290     0.8857 0.000 0.992 0.008 0.000 0.000
#&gt; SRR1946662     5  0.2374     0.8543 0.020 0.052 0.016 0.000 0.912
#&gt; SRR1946661     5  0.3183     0.7968 0.000 0.156 0.016 0.000 0.828
#&gt; SRR1946660     2  0.2471     0.7871 0.000 0.864 0.000 0.000 0.136
#&gt; SRR1946659     1  0.0000     0.9026 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946658     5  0.1341     0.8342 0.000 0.056 0.000 0.000 0.944
#&gt; SRR1946657     2  0.0609     0.8866 0.000 0.980 0.020 0.000 0.000
#&gt; SRR1946655     3  0.0510     0.8585 0.000 0.016 0.984 0.000 0.000
#&gt; SRR1946654     3  0.0451     0.8585 0.000 0.008 0.988 0.000 0.004
#&gt; SRR1946653     3  0.1043     0.8533 0.040 0.000 0.960 0.000 0.000
#&gt; SRR1946652     2  0.1549     0.8563 0.000 0.944 0.016 0.000 0.040
#&gt; SRR1946651     2  0.0693     0.8851 0.000 0.980 0.008 0.000 0.012
#&gt; SRR1946650     2  0.0771     0.8830 0.000 0.976 0.004 0.000 0.020
#&gt; SRR1946649     1  0.5915     0.3653 0.588 0.324 0.048 0.000 0.040
#&gt; SRR1946648     3  0.3177     0.6979 0.000 0.000 0.792 0.000 0.208
#&gt; SRR1946647     5  0.2409     0.8488 0.032 0.000 0.068 0.000 0.900
#&gt; SRR1946646     3  0.0880     0.8559 0.000 0.032 0.968 0.000 0.000
#&gt; SRR1946645     1  0.4398     0.5755 0.720 0.000 0.240 0.000 0.040
#&gt; SRR1946644     2  0.0609     0.8866 0.000 0.980 0.020 0.000 0.000
#&gt; SRR1946643     3  0.0510     0.8585 0.000 0.016 0.984 0.000 0.000
#&gt; SRR1946642     1  0.0000     0.9026 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.9026 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0510     0.8585 0.000 0.016 0.984 0.000 0.000
#&gt; SRR1946640     1  0.0000     0.9026 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.9026 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9026 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9026 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5    p6
#&gt; SRR1946675     3  0.0632   0.846943 0.000 0.000 0.976  0 0.024 0.000
#&gt; SRR1946691     6  0.0000   0.912514 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1946690     2  0.1910   0.787714 0.000 0.892 0.000  0 0.000 0.108
#&gt; SRR1946689     4  0.0000   1.000000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946686     3  0.0632   0.848035 0.024 0.000 0.976  0 0.000 0.000
#&gt; SRR1946685     2  0.3847   0.070101 0.000 0.544 0.456  0 0.000 0.000
#&gt; SRR1946688     6  0.0000   0.912514 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1946684     5  0.0000   0.791046 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946683     5  0.4859   0.603866 0.016 0.104 0.188  0 0.692 0.000
#&gt; SRR1946682     6  0.2378   0.832600 0.000 0.000 0.000  0 0.152 0.848
#&gt; SRR1946680     4  0.0000   1.000000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946681     3  0.3860  -0.000579 0.000 0.472 0.528  0 0.000 0.000
#&gt; SRR1946687     3  0.0820   0.849548 0.016 0.000 0.972  0 0.012 0.000
#&gt; SRR1946679     2  0.0000   0.814235 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1946678     1  0.0000   0.880895 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946676     3  0.4409   0.381355 0.000 0.380 0.588  0 0.032 0.000
#&gt; SRR1946677     5  0.4678   0.650899 0.020 0.132 0.124  0 0.724 0.000
#&gt; SRR1946672     3  0.0000   0.850588 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946673     5  0.2562   0.670416 0.000 0.172 0.000  0 0.828 0.000
#&gt; SRR1946671     3  0.6440  -0.005703 0.028 0.196 0.400  0 0.376 0.000
#&gt; SRR1946669     5  0.0790   0.781918 0.032 0.000 0.000  0 0.968 0.000
#&gt; SRR1946668     5  0.0547   0.787346 0.020 0.000 0.000  0 0.980 0.000
#&gt; SRR1946666     3  0.0937   0.838735 0.040 0.000 0.960  0 0.000 0.000
#&gt; SRR1946667     4  0.0000   1.000000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946670     5  0.4366   0.352394 0.000 0.000 0.024  0 0.548 0.428
#&gt; SRR1946663     6  0.1910   0.869508 0.000 0.000 0.000  0 0.108 0.892
#&gt; SRR1946664     2  0.1910   0.787714 0.000 0.892 0.000  0 0.000 0.108
#&gt; SRR1946662     5  0.0000   0.791046 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946661     5  0.1863   0.752991 0.000 0.104 0.000  0 0.896 0.000
#&gt; SRR1946660     6  0.0000   0.912514 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1946659     1  0.0000   0.880895 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946658     5  0.4439   0.330347 0.000 0.028 0.000  0 0.540 0.432
#&gt; SRR1946657     2  0.1910   0.789460 0.000 0.892 0.108  0 0.000 0.000
#&gt; SRR1946655     3  0.0000   0.850588 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946654     3  0.0622   0.850276 0.000 0.012 0.980  0 0.008 0.000
#&gt; SRR1946653     3  0.0632   0.848035 0.024 0.000 0.976  0 0.000 0.000
#&gt; SRR1946652     2  0.2562   0.647164 0.000 0.828 0.000  0 0.172 0.000
#&gt; SRR1946651     2  0.0000   0.814235 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1946650     2  0.0260   0.811527 0.000 0.992 0.000  0 0.008 0.000
#&gt; SRR1946649     1  0.5972   0.280951 0.492 0.324 0.012  0 0.172 0.000
#&gt; SRR1946648     3  0.3221   0.611044 0.000 0.000 0.736  0 0.264 0.000
#&gt; SRR1946647     5  0.0000   0.791046 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946646     3  0.0632   0.845892 0.000 0.024 0.976  0 0.000 0.000
#&gt; SRR1946645     1  0.6414   0.426617 0.568 0.104 0.156  0 0.172 0.000
#&gt; SRR1946644     2  0.1910   0.789460 0.000 0.892 0.108  0 0.000 0.000
#&gt; SRR1946643     3  0.0000   0.850588 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946642     1  0.0000   0.880895 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946641     1  0.0000   0.880895 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946656     3  0.0000   0.850588 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946640     1  0.0000   0.880895 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946639     1  0.0000   0.880895 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946638     1  0.0000   0.880895 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946637     1  0.0000   0.880895 1.000 0.000 0.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.473           0.799       0.852          0.397 0.643   0.643
#> 3 3 0.214           0.581       0.721          0.394 0.623   0.472
#> 4 4 0.434           0.569       0.762          0.083 0.592   0.309
#> 5 5 0.503           0.726       0.721          0.175 0.797   0.496
#> 6 6 0.646           0.562       0.742          0.115 0.848   0.550
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1   0.808      0.794 0.752 0.248
#&gt; SRR1946691     2   0.844      0.897 0.272 0.728
#&gt; SRR1946690     2   0.871      0.881 0.292 0.708
#&gt; SRR1946689     2   0.163      0.721 0.024 0.976
#&gt; SRR1946686     1   0.808      0.794 0.752 0.248
#&gt; SRR1946685     1   0.000      0.823 1.000 0.000
#&gt; SRR1946688     2   0.844      0.897 0.272 0.728
#&gt; SRR1946684     1   0.730      0.537 0.796 0.204
#&gt; SRR1946683     1   0.000      0.823 1.000 0.000
#&gt; SRR1946682     2   0.844      0.897 0.272 0.728
#&gt; SRR1946680     2   0.163      0.721 0.024 0.976
#&gt; SRR1946681     1   0.000      0.823 1.000 0.000
#&gt; SRR1946687     1   0.808      0.794 0.752 0.248
#&gt; SRR1946679     1   0.000      0.823 1.000 0.000
#&gt; SRR1946678     1   0.430      0.822 0.912 0.088
#&gt; SRR1946676     1   0.000      0.823 1.000 0.000
#&gt; SRR1946677     1   0.000      0.823 1.000 0.000
#&gt; SRR1946672     1   0.808      0.794 0.752 0.248
#&gt; SRR1946673     1   0.000      0.823 1.000 0.000
#&gt; SRR1946671     1   0.000      0.823 1.000 0.000
#&gt; SRR1946669     1   0.000      0.823 1.000 0.000
#&gt; SRR1946668     1   0.000      0.823 1.000 0.000
#&gt; SRR1946666     1   0.808      0.794 0.752 0.248
#&gt; SRR1946667     2   0.163      0.721 0.024 0.976
#&gt; SRR1946670     2   0.844      0.897 0.272 0.728
#&gt; SRR1946663     2   0.844      0.897 0.272 0.728
#&gt; SRR1946664     2   0.917      0.835 0.332 0.668
#&gt; SRR1946662     1   0.000      0.823 1.000 0.000
#&gt; SRR1946661     1   0.430      0.736 0.912 0.088
#&gt; SRR1946660     2   0.844      0.897 0.272 0.728
#&gt; SRR1946659     1   0.808      0.794 0.752 0.248
#&gt; SRR1946658     2   0.844      0.897 0.272 0.728
#&gt; SRR1946657     1   0.000      0.823 1.000 0.000
#&gt; SRR1946655     1   0.808      0.794 0.752 0.248
#&gt; SRR1946654     1   0.808      0.794 0.752 0.248
#&gt; SRR1946653     1   0.808      0.794 0.752 0.248
#&gt; SRR1946652     1   0.000      0.823 1.000 0.000
#&gt; SRR1946651     1   0.615      0.637 0.848 0.152
#&gt; SRR1946650     1   0.814      0.412 0.748 0.252
#&gt; SRR1946649     1   0.000      0.823 1.000 0.000
#&gt; SRR1946648     1   0.662      0.811 0.828 0.172
#&gt; SRR1946647     1   0.000      0.823 1.000 0.000
#&gt; SRR1946646     1   0.358      0.825 0.932 0.068
#&gt; SRR1946645     1   0.000      0.823 1.000 0.000
#&gt; SRR1946644     1   0.184      0.801 0.972 0.028
#&gt; SRR1946643     1   0.808      0.794 0.752 0.248
#&gt; SRR1946642     1   0.430      0.822 0.912 0.088
#&gt; SRR1946641     1   0.844      0.780 0.728 0.272
#&gt; SRR1946656     1   0.808      0.794 0.752 0.248
#&gt; SRR1946640     1   0.844      0.780 0.728 0.272
#&gt; SRR1946639     1   0.844      0.780 0.728 0.272
#&gt; SRR1946638     1   0.844      0.780 0.728 0.272
#&gt; SRR1946637     1   0.844      0.780 0.728 0.272
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     1  0.4526     0.6839 0.856 0.104 0.040
#&gt; SRR1946691     2  0.3784     0.7300 0.132 0.864 0.004
#&gt; SRR1946690     2  0.4047     0.7304 0.148 0.848 0.004
#&gt; SRR1946689     3  0.6854     0.7921 0.136 0.124 0.740
#&gt; SRR1946686     1  0.4172     0.6873 0.868 0.104 0.028
#&gt; SRR1946685     1  0.6473     0.6341 0.652 0.332 0.016
#&gt; SRR1946688     2  0.3784     0.7300 0.132 0.864 0.004
#&gt; SRR1946684     2  0.0983     0.6767 0.016 0.980 0.004
#&gt; SRR1946683     1  0.5497     0.6834 0.708 0.292 0.000
#&gt; SRR1946682     2  0.3965     0.7286 0.132 0.860 0.008
#&gt; SRR1946680     3  0.7147     0.7928 0.156 0.124 0.720
#&gt; SRR1946681     1  0.8600     0.4552 0.604 0.212 0.184
#&gt; SRR1946687     1  0.8808    -0.0633 0.536 0.132 0.332
#&gt; SRR1946679     2  0.6952    -0.2808 0.480 0.504 0.016
#&gt; SRR1946678     1  0.4677     0.6225 0.840 0.028 0.132
#&gt; SRR1946676     1  0.6313     0.6422 0.676 0.308 0.016
#&gt; SRR1946677     1  0.5926     0.6412 0.644 0.356 0.000
#&gt; SRR1946672     1  0.6111     0.6305 0.784 0.104 0.112
#&gt; SRR1946673     1  0.6295     0.4370 0.528 0.472 0.000
#&gt; SRR1946671     1  0.6057     0.6571 0.656 0.340 0.004
#&gt; SRR1946669     1  0.5882     0.6487 0.652 0.348 0.000
#&gt; SRR1946668     2  0.5404     0.4099 0.256 0.740 0.004
#&gt; SRR1946666     1  0.4295     0.6868 0.864 0.104 0.032
#&gt; SRR1946667     3  0.6854     0.7921 0.136 0.124 0.740
#&gt; SRR1946670     2  0.3784     0.7300 0.132 0.864 0.004
#&gt; SRR1946663     2  0.3784     0.7300 0.132 0.864 0.004
#&gt; SRR1946664     2  0.6393     0.6561 0.148 0.764 0.088
#&gt; SRR1946662     1  0.6305     0.4067 0.516 0.484 0.000
#&gt; SRR1946661     2  0.1163     0.6782 0.028 0.972 0.000
#&gt; SRR1946660     2  0.3784     0.7300 0.132 0.864 0.004
#&gt; SRR1946659     1  0.4295     0.6868 0.864 0.104 0.032
#&gt; SRR1946658     2  0.3686     0.7311 0.140 0.860 0.000
#&gt; SRR1946657     2  0.6448     0.4934 0.328 0.656 0.016
#&gt; SRR1946655     3  0.6081     0.6669 0.344 0.004 0.652
#&gt; SRR1946654     1  0.5892     0.6440 0.796 0.104 0.100
#&gt; SRR1946653     1  0.8676    -0.0929 0.520 0.112 0.368
#&gt; SRR1946652     2  0.5621     0.4297 0.308 0.692 0.000
#&gt; SRR1946651     2  0.6848     0.1978 0.416 0.568 0.016
#&gt; SRR1946650     2  0.1643     0.6878 0.044 0.956 0.000
#&gt; SRR1946649     1  0.6008     0.6228 0.628 0.372 0.000
#&gt; SRR1946648     1  0.4324     0.6898 0.860 0.112 0.028
#&gt; SRR1946647     2  0.6282     0.0518 0.384 0.612 0.004
#&gt; SRR1946646     1  0.4033     0.6940 0.856 0.136 0.008
#&gt; SRR1946645     1  0.5465     0.6847 0.712 0.288 0.000
#&gt; SRR1946644     2  0.4883     0.7041 0.208 0.788 0.004
#&gt; SRR1946643     3  0.6468     0.4148 0.444 0.004 0.552
#&gt; SRR1946642     1  0.4799     0.6237 0.836 0.032 0.132
#&gt; SRR1946641     1  0.3752     0.6077 0.856 0.000 0.144
#&gt; SRR1946656     3  0.4293     0.7467 0.164 0.004 0.832
#&gt; SRR1946640     1  0.3752     0.6077 0.856 0.000 0.144
#&gt; SRR1946639     1  0.3752     0.6077 0.856 0.000 0.144
#&gt; SRR1946638     1  0.3752     0.6077 0.856 0.000 0.144
#&gt; SRR1946637     1  0.3752     0.6077 0.856 0.000 0.144
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.4224      0.727 0.100 0.076 0.824 0.000
#&gt; SRR1946691     2  0.5949      0.401 0.004 0.484 0.484 0.028
#&gt; SRR1946690     3  0.5677     -0.439 0.004 0.476 0.504 0.016
#&gt; SRR1946689     4  0.1389      1.000 0.000 0.000 0.048 0.952
#&gt; SRR1946686     3  0.5431      0.662 0.224 0.064 0.712 0.000
#&gt; SRR1946685     2  0.5143      0.544 0.012 0.628 0.360 0.000
#&gt; SRR1946688     2  0.6314      0.428 0.004 0.484 0.464 0.048
#&gt; SRR1946684     2  0.1516      0.628 0.016 0.960 0.016 0.008
#&gt; SRR1946683     2  0.1042      0.625 0.020 0.972 0.000 0.008
#&gt; SRR1946682     2  0.6314      0.428 0.004 0.484 0.464 0.048
#&gt; SRR1946680     3  0.3958      0.678 0.000 0.032 0.824 0.144
#&gt; SRR1946681     3  0.5795     -0.305 0.016 0.460 0.516 0.008
#&gt; SRR1946687     3  0.4058      0.693 0.016 0.028 0.840 0.116
#&gt; SRR1946679     2  0.5007      0.548 0.008 0.636 0.356 0.000
#&gt; SRR1946678     1  0.3688      0.669 0.792 0.208 0.000 0.000
#&gt; SRR1946676     2  0.5143      0.544 0.012 0.628 0.360 0.000
#&gt; SRR1946677     2  0.1042      0.625 0.020 0.972 0.000 0.008
#&gt; SRR1946672     3  0.4007      0.729 0.068 0.056 0.856 0.020
#&gt; SRR1946673     2  0.0188      0.632 0.004 0.996 0.000 0.000
#&gt; SRR1946671     2  0.4082      0.626 0.020 0.820 0.152 0.008
#&gt; SRR1946669     2  0.1389      0.611 0.048 0.952 0.000 0.000
#&gt; SRR1946668     2  0.1739      0.628 0.024 0.952 0.016 0.008
#&gt; SRR1946666     3  0.4282      0.724 0.124 0.060 0.816 0.000
#&gt; SRR1946667     4  0.1389      1.000 0.000 0.000 0.048 0.952
#&gt; SRR1946670     2  0.6248      0.424 0.004 0.484 0.468 0.044
#&gt; SRR1946663     2  0.6314      0.428 0.004 0.484 0.464 0.048
#&gt; SRR1946664     3  0.6021     -0.438 0.016 0.476 0.492 0.016
#&gt; SRR1946662     2  0.0188      0.632 0.004 0.996 0.000 0.000
#&gt; SRR1946661     2  0.1443      0.629 0.004 0.960 0.028 0.008
#&gt; SRR1946660     2  0.6314      0.428 0.004 0.484 0.464 0.048
#&gt; SRR1946659     3  0.4372      0.728 0.104 0.056 0.828 0.012
#&gt; SRR1946658     3  0.5679     -0.445 0.004 0.484 0.496 0.016
#&gt; SRR1946657     2  0.5024      0.545 0.008 0.632 0.360 0.000
#&gt; SRR1946655     3  0.3622      0.703 0.064 0.012 0.872 0.052
#&gt; SRR1946654     3  0.3805      0.730 0.068 0.072 0.856 0.004
#&gt; SRR1946653     3  0.4277      0.713 0.052 0.028 0.844 0.076
#&gt; SRR1946652     2  0.4679      0.549 0.000 0.648 0.352 0.000
#&gt; SRR1946651     2  0.4936      0.543 0.000 0.624 0.372 0.004
#&gt; SRR1946650     2  0.4781      0.568 0.004 0.660 0.336 0.000
#&gt; SRR1946649     2  0.1042      0.625 0.020 0.972 0.000 0.008
#&gt; SRR1946648     3  0.4724      0.706 0.096 0.112 0.792 0.000
#&gt; SRR1946647     2  0.2282      0.626 0.052 0.924 0.024 0.000
#&gt; SRR1946646     3  0.6363      0.480 0.108 0.236 0.652 0.004
#&gt; SRR1946645     2  0.3472      0.632 0.024 0.868 0.100 0.008
#&gt; SRR1946644     2  0.6394      0.452 0.048 0.528 0.416 0.008
#&gt; SRR1946643     3  0.3622      0.703 0.064 0.012 0.872 0.052
#&gt; SRR1946642     1  0.3356      0.702 0.824 0.176 0.000 0.000
#&gt; SRR1946641     1  0.0804      0.881 0.980 0.008 0.012 0.000
#&gt; SRR1946656     3  0.3622      0.703 0.064 0.012 0.872 0.052
#&gt; SRR1946640     1  0.0804      0.881 0.980 0.008 0.012 0.000
#&gt; SRR1946639     1  0.0804      0.881 0.980 0.008 0.012 0.000
#&gt; SRR1946638     1  0.0804      0.881 0.980 0.008 0.012 0.000
#&gt; SRR1946637     1  0.0804      0.881 0.980 0.008 0.012 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.5060      0.833 0.104 0.204 0.692 0.000 0.000
#&gt; SRR1946691     2  0.3370      0.601 0.000 0.824 0.148 0.000 0.028
#&gt; SRR1946690     2  0.4679      0.597 0.000 0.716 0.216 0.000 0.068
#&gt; SRR1946689     4  0.0290      1.000 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1946686     3  0.5444      0.828 0.140 0.204 0.656 0.000 0.000
#&gt; SRR1946685     2  0.5935      0.448 0.000 0.516 0.084 0.008 0.392
#&gt; SRR1946688     2  0.0955      0.607 0.000 0.968 0.004 0.000 0.028
#&gt; SRR1946684     5  0.3741      0.765 0.004 0.264 0.000 0.000 0.732
#&gt; SRR1946683     5  0.0162      0.778 0.000 0.000 0.004 0.000 0.996
#&gt; SRR1946682     2  0.0955      0.607 0.000 0.968 0.004 0.000 0.028
#&gt; SRR1946680     3  0.5822      0.649 0.004 0.324 0.572 0.100 0.000
#&gt; SRR1946681     2  0.6113      0.386 0.000 0.508 0.372 0.004 0.116
#&gt; SRR1946687     3  0.5322      0.826 0.112 0.228 0.660 0.000 0.000
#&gt; SRR1946679     2  0.5913      0.464 0.000 0.528 0.084 0.008 0.380
#&gt; SRR1946678     1  0.1270      0.941 0.948 0.000 0.000 0.000 0.052
#&gt; SRR1946676     2  0.6501      0.586 0.000 0.524 0.184 0.008 0.284
#&gt; SRR1946677     5  0.0510      0.781 0.000 0.016 0.000 0.000 0.984
#&gt; SRR1946672     3  0.3143      0.796 0.000 0.204 0.796 0.000 0.000
#&gt; SRR1946673     5  0.3048      0.820 0.000 0.176 0.004 0.000 0.820
#&gt; SRR1946671     5  0.2672      0.721 0.004 0.116 0.008 0.000 0.872
#&gt; SRR1946669     5  0.3880      0.814 0.028 0.184 0.004 0.000 0.784
#&gt; SRR1946668     5  0.3527      0.818 0.024 0.172 0.000 0.000 0.804
#&gt; SRR1946666     3  0.5496      0.824 0.152 0.196 0.652 0.000 0.000
#&gt; SRR1946667     4  0.0290      1.000 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1946670     2  0.1830      0.612 0.000 0.932 0.040 0.000 0.028
#&gt; SRR1946663     2  0.0955      0.607 0.000 0.968 0.004 0.000 0.028
#&gt; SRR1946664     2  0.4619      0.595 0.000 0.720 0.216 0.000 0.064
#&gt; SRR1946662     5  0.3048      0.820 0.000 0.176 0.004 0.000 0.820
#&gt; SRR1946661     5  0.3336      0.769 0.000 0.228 0.000 0.000 0.772
#&gt; SRR1946660     2  0.0955      0.607 0.000 0.968 0.004 0.000 0.028
#&gt; SRR1946659     3  0.5496      0.824 0.152 0.196 0.652 0.000 0.000
#&gt; SRR1946658     2  0.4767      0.612 0.000 0.720 0.192 0.000 0.088
#&gt; SRR1946657     2  0.6520      0.597 0.000 0.528 0.200 0.008 0.264
#&gt; SRR1946655     3  0.1851      0.740 0.000 0.088 0.912 0.000 0.000
#&gt; SRR1946654     3  0.3143      0.796 0.000 0.204 0.796 0.000 0.000
#&gt; SRR1946653     3  0.5365      0.832 0.132 0.204 0.664 0.000 0.000
#&gt; SRR1946652     2  0.5654      0.478 0.000 0.536 0.084 0.000 0.380
#&gt; SRR1946651     2  0.5855      0.516 0.000 0.536 0.108 0.000 0.356
#&gt; SRR1946650     2  0.4818      0.267 0.000 0.520 0.020 0.000 0.460
#&gt; SRR1946649     5  0.0963      0.784 0.000 0.036 0.000 0.000 0.964
#&gt; SRR1946648     3  0.5594      0.830 0.128 0.204 0.660 0.000 0.008
#&gt; SRR1946647     5  0.4394      0.719 0.036 0.228 0.004 0.000 0.732
#&gt; SRR1946646     3  0.5230      0.706 0.000 0.240 0.676 0.008 0.076
#&gt; SRR1946645     5  0.3063      0.719 0.036 0.096 0.004 0.000 0.864
#&gt; SRR1946644     2  0.5785      0.480 0.000 0.568 0.320 0.000 0.112
#&gt; SRR1946643     3  0.0162      0.642 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1946642     1  0.1704      0.919 0.928 0.004 0.000 0.000 0.068
#&gt; SRR1946641     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0162      0.642 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1946640     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0162      0.972 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946638     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR1946675     3  0.3073    0.72394 0.204 0.000 0.788 0.000 NA 0.000
#&gt; SRR1946691     6  0.5205    0.51637 0.000 0.224 0.124 0.000 NA 0.640
#&gt; SRR1946690     2  0.5951   -0.33693 0.000 0.456 0.128 0.000 NA 0.396
#&gt; SRR1946689     4  0.0000    1.00000 0.000 0.000 0.000 1.000 NA 0.000
#&gt; SRR1946686     3  0.2994    0.72368 0.208 0.000 0.788 0.000 NA 0.000
#&gt; SRR1946685     2  0.3351    0.41787 0.000 0.828 0.120 0.000 NA 0.024
#&gt; SRR1946688     6  0.0146    0.76448 0.000 0.004 0.000 0.000 NA 0.996
#&gt; SRR1946684     2  0.4509    0.58205 0.000 0.532 0.000 0.000 NA 0.032
#&gt; SRR1946683     2  0.3991    0.58134 0.004 0.524 0.000 0.000 NA 0.000
#&gt; SRR1946682     6  0.0146    0.76448 0.000 0.004 0.000 0.000 NA 0.996
#&gt; SRR1946680     3  0.7759    0.20132 0.004 0.008 0.384 0.232 NA 0.164
#&gt; SRR1946681     2  0.7380   -0.15392 0.004 0.352 0.232 0.000 NA 0.100
#&gt; SRR1946687     3  0.3043    0.72519 0.200 0.000 0.792 0.000 NA 0.000
#&gt; SRR1946679     2  0.2804    0.41481 0.000 0.852 0.120 0.000 NA 0.024
#&gt; SRR1946678     1  0.2980    0.70431 0.800 0.008 0.000 0.000 NA 0.000
#&gt; SRR1946676     2  0.3192    0.41262 0.000 0.836 0.120 0.000 NA 0.024
#&gt; SRR1946677     2  0.3847    0.59045 0.000 0.544 0.000 0.000 NA 0.000
#&gt; SRR1946672     3  0.0603    0.68755 0.016 0.004 0.980 0.000 NA 0.000
#&gt; SRR1946673     2  0.3782    0.60098 0.000 0.588 0.000 0.000 NA 0.000
#&gt; SRR1946671     2  0.3860    0.58241 0.000 0.528 0.000 0.000 NA 0.000
#&gt; SRR1946669     2  0.4018    0.60055 0.008 0.580 0.000 0.000 NA 0.000
#&gt; SRR1946668     2  0.3862    0.59350 0.000 0.524 0.000 0.000 NA 0.000
#&gt; SRR1946666     3  0.2883    0.72319 0.212 0.000 0.788 0.000 NA 0.000
#&gt; SRR1946667     4  0.0000    1.00000 0.000 0.000 0.000 1.000 NA 0.000
#&gt; SRR1946670     6  0.1536    0.74228 0.000 0.004 0.040 0.000 NA 0.940
#&gt; SRR1946663     6  0.0146    0.76448 0.000 0.004 0.000 0.000 NA 0.996
#&gt; SRR1946664     2  0.5948   -0.33221 0.000 0.460 0.128 0.000 NA 0.392
#&gt; SRR1946662     2  0.3789    0.60114 0.000 0.584 0.000 0.000 NA 0.000
#&gt; SRR1946661     2  0.3986    0.59041 0.000 0.532 0.000 0.000 NA 0.004
#&gt; SRR1946660     6  0.0146    0.76448 0.000 0.004 0.000 0.000 NA 0.996
#&gt; SRR1946659     3  0.2883    0.72319 0.212 0.000 0.788 0.000 NA 0.000
#&gt; SRR1946658     6  0.7407    0.16993 0.000 0.292 0.128 0.000 NA 0.352
#&gt; SRR1946657     2  0.2662    0.41190 0.000 0.856 0.120 0.000 NA 0.024
#&gt; SRR1946655     3  0.4076    0.36233 0.000 0.004 0.564 0.000 NA 0.004
#&gt; SRR1946654     3  0.0603    0.68755 0.016 0.004 0.980 0.000 NA 0.000
#&gt; SRR1946653     3  0.3012    0.72556 0.196 0.000 0.796 0.000 NA 0.000
#&gt; SRR1946652     2  0.3015    0.41633 0.000 0.844 0.120 0.000 NA 0.024
#&gt; SRR1946651     2  0.3496    0.39708 0.000 0.820 0.120 0.000 NA 0.024
#&gt; SRR1946650     2  0.4795    0.56600 0.000 0.588 0.024 0.000 NA 0.024
#&gt; SRR1946649     2  0.3843    0.59236 0.000 0.548 0.000 0.000 NA 0.000
#&gt; SRR1946648     3  0.3522    0.62568 0.044 0.000 0.784 0.000 NA 0.000
#&gt; SRR1946647     2  0.4096    0.59201 0.000 0.508 0.008 0.000 NA 0.000
#&gt; SRR1946646     3  0.4176    0.59078 0.004 0.196 0.748 0.000 NA 0.024
#&gt; SRR1946645     2  0.4335    0.58753 0.000 0.508 0.020 0.000 NA 0.000
#&gt; SRR1946644     2  0.6730    0.00958 0.000 0.508 0.244 0.000 NA 0.124
#&gt; SRR1946643     3  0.4076    0.36233 0.000 0.004 0.564 0.000 NA 0.004
#&gt; SRR1946642     1  0.3217    0.66061 0.768 0.008 0.000 0.000 NA 0.000
#&gt; SRR1946641     1  0.0000    0.88198 1.000 0.000 0.000 0.000 NA 0.000
#&gt; SRR1946656     3  0.4076    0.36233 0.000 0.004 0.564 0.000 NA 0.004
#&gt; SRR1946640     1  0.0000    0.88198 1.000 0.000 0.000 0.000 NA 0.000
#&gt; SRR1946639     1  0.0146    0.87898 0.996 0.000 0.000 0.000 NA 0.000
#&gt; SRR1946638     1  0.0000    0.88198 1.000 0.000 0.000 0.000 NA 0.000
#&gt; SRR1946637     1  0.0000    0.88198 1.000 0.000 0.000 0.000 NA 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.589           0.823       0.924         0.4911 0.492   0.492
#> 3 3 0.767           0.842       0.936         0.3081 0.647   0.410
#> 4 4 0.566           0.700       0.838         0.1332 0.744   0.416
#> 5 5 0.712           0.726       0.866         0.0977 0.759   0.320
#> 6 6 0.760           0.655       0.837         0.0479 0.884   0.509
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1   0.861     0.5933 0.716 0.284
#&gt; SRR1946691     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946690     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946689     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946686     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946685     1   0.866     0.5856 0.712 0.288
#&gt; SRR1946688     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946684     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946683     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946682     2   0.722     0.7693 0.200 0.800
#&gt; SRR1946680     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946681     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946687     1   0.760     0.6983 0.780 0.220
#&gt; SRR1946679     2   0.653     0.8024 0.168 0.832
#&gt; SRR1946678     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946676     2   0.943     0.4841 0.360 0.640
#&gt; SRR1946677     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946672     1   0.988     0.1951 0.564 0.436
#&gt; SRR1946673     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946671     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946669     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946668     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946666     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946667     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946670     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946663     2   0.955     0.4448 0.376 0.624
#&gt; SRR1946664     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946662     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946661     1   0.653     0.7650 0.832 0.168
#&gt; SRR1946660     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946659     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946658     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946657     2   0.416     0.8612 0.084 0.916
#&gt; SRR1946655     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946654     2   0.706     0.7780 0.192 0.808
#&gt; SRR1946653     2   0.827     0.6869 0.260 0.740
#&gt; SRR1946652     2   0.788     0.7231 0.236 0.764
#&gt; SRR1946651     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946650     1   0.998     0.0492 0.528 0.472
#&gt; SRR1946649     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946648     1   0.625     0.7782 0.844 0.156
#&gt; SRR1946647     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946646     2   0.595     0.8218 0.144 0.856
#&gt; SRR1946645     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946644     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946643     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946642     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946641     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946656     2   0.000     0.9032 0.000 1.000
#&gt; SRR1946640     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946639     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946638     1   0.000     0.9123 1.000 0.000
#&gt; SRR1946637     1   0.000     0.9123 1.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     1  0.6280     0.0455 0.540 0.000 0.460
#&gt; SRR1946691     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946690     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946689     3  0.0000     0.9160 0.000 0.000 1.000
#&gt; SRR1946686     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946685     2  0.1753     0.9247 0.048 0.952 0.000
#&gt; SRR1946688     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946684     2  0.4842     0.7060 0.224 0.776 0.000
#&gt; SRR1946683     1  0.0747     0.8674 0.984 0.016 0.000
#&gt; SRR1946682     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946680     3  0.0000     0.9160 0.000 0.000 1.000
#&gt; SRR1946681     2  0.4178     0.8056 0.000 0.828 0.172
#&gt; SRR1946687     3  0.5178     0.6647 0.256 0.000 0.744
#&gt; SRR1946679     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946678     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946676     2  0.0237     0.9509 0.004 0.996 0.000
#&gt; SRR1946677     2  0.0747     0.9450 0.016 0.984 0.000
#&gt; SRR1946672     3  0.2625     0.8711 0.084 0.000 0.916
#&gt; SRR1946673     2  0.2356     0.9041 0.072 0.928 0.000
#&gt; SRR1946671     1  0.6267     0.1812 0.548 0.452 0.000
#&gt; SRR1946669     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946668     1  0.6302     0.0874 0.520 0.480 0.000
#&gt; SRR1946666     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946667     3  0.0000     0.9160 0.000 0.000 1.000
#&gt; SRR1946670     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946663     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946664     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946662     2  0.3482     0.8474 0.128 0.872 0.000
#&gt; SRR1946661     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946660     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946659     1  0.0592     0.8691 0.988 0.000 0.012
#&gt; SRR1946658     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946657     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946655     3  0.0000     0.9160 0.000 0.000 1.000
#&gt; SRR1946654     3  0.0592     0.9122 0.012 0.000 0.988
#&gt; SRR1946653     3  0.4555     0.7482 0.200 0.000 0.800
#&gt; SRR1946652     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946651     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946650     2  0.0000     0.9528 0.000 1.000 0.000
#&gt; SRR1946649     2  0.3340     0.8578 0.120 0.880 0.000
#&gt; SRR1946648     1  0.2261     0.8242 0.932 0.000 0.068
#&gt; SRR1946647     1  0.4121     0.7223 0.832 0.168 0.000
#&gt; SRR1946646     3  0.4915     0.7486 0.012 0.184 0.804
#&gt; SRR1946645     1  0.0237     0.8750 0.996 0.004 0.000
#&gt; SRR1946644     2  0.4750     0.7199 0.000 0.784 0.216
#&gt; SRR1946643     3  0.0000     0.9160 0.000 0.000 1.000
#&gt; SRR1946642     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946656     3  0.0000     0.9160 0.000 0.000 1.000
#&gt; SRR1946640     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.8768 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.8768 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     1  0.6858     0.2783 0.532 0.004 0.096 0.368
#&gt; SRR1946691     2  0.3435     0.6699 0.000 0.864 0.100 0.036
#&gt; SRR1946690     3  0.2868     0.7487 0.000 0.136 0.864 0.000
#&gt; SRR1946689     4  0.3873     0.7673 0.000 0.228 0.000 0.772
#&gt; SRR1946686     1  0.2530     0.7554 0.896 0.000 0.004 0.100
#&gt; SRR1946685     3  0.0336     0.7988 0.000 0.008 0.992 0.000
#&gt; SRR1946688     2  0.1004     0.7575 0.000 0.972 0.004 0.024
#&gt; SRR1946684     2  0.4053     0.7818 0.228 0.768 0.004 0.000
#&gt; SRR1946683     1  0.2053     0.7679 0.924 0.072 0.004 0.000
#&gt; SRR1946682     2  0.0376     0.7709 0.000 0.992 0.004 0.004
#&gt; SRR1946680     4  0.3497     0.7701 0.000 0.124 0.024 0.852
#&gt; SRR1946681     3  0.0336     0.7938 0.000 0.000 0.992 0.008
#&gt; SRR1946687     4  0.4361     0.6540 0.208 0.020 0.000 0.772
#&gt; SRR1946679     3  0.1792     0.7875 0.000 0.068 0.932 0.000
#&gt; SRR1946678     1  0.0188     0.8125 0.996 0.004 0.000 0.000
#&gt; SRR1946676     3  0.0592     0.7993 0.000 0.016 0.984 0.000
#&gt; SRR1946677     2  0.4719     0.7977 0.180 0.772 0.048 0.000
#&gt; SRR1946672     1  0.7472     0.2959 0.504 0.000 0.264 0.232
#&gt; SRR1946673     2  0.5222     0.7830 0.112 0.756 0.132 0.000
#&gt; SRR1946671     1  0.5200     0.5958 0.744 0.184 0.072 0.000
#&gt; SRR1946669     2  0.4697     0.6258 0.356 0.644 0.000 0.000
#&gt; SRR1946668     2  0.3942     0.7761 0.236 0.764 0.000 0.000
#&gt; SRR1946666     1  0.1118     0.8005 0.964 0.000 0.000 0.036
#&gt; SRR1946667     4  0.3873     0.7673 0.000 0.228 0.000 0.772
#&gt; SRR1946670     2  0.0188     0.7721 0.000 0.996 0.004 0.000
#&gt; SRR1946663     2  0.1004     0.7590 0.000 0.972 0.004 0.024
#&gt; SRR1946664     3  0.2814     0.7517 0.000 0.132 0.868 0.000
#&gt; SRR1946662     2  0.5346     0.7799 0.192 0.732 0.076 0.000
#&gt; SRR1946661     2  0.4181     0.8094 0.128 0.820 0.052 0.000
#&gt; SRR1946660     2  0.1182     0.7695 0.000 0.968 0.016 0.016
#&gt; SRR1946659     1  0.3610     0.6636 0.800 0.000 0.000 0.200
#&gt; SRR1946658     2  0.3837     0.7207 0.000 0.776 0.224 0.000
#&gt; SRR1946657     3  0.1022     0.7974 0.000 0.032 0.968 0.000
#&gt; SRR1946655     3  0.4999     0.1967 0.000 0.000 0.508 0.492
#&gt; SRR1946654     3  0.7031     0.3686 0.224 0.000 0.576 0.200
#&gt; SRR1946653     4  0.3710     0.6462 0.192 0.000 0.004 0.804
#&gt; SRR1946652     3  0.4605     0.4317 0.000 0.336 0.664 0.000
#&gt; SRR1946651     3  0.3444     0.6999 0.000 0.184 0.816 0.000
#&gt; SRR1946650     2  0.4158     0.7225 0.008 0.768 0.224 0.000
#&gt; SRR1946649     1  0.7778     0.0902 0.420 0.256 0.324 0.000
#&gt; SRR1946648     1  0.6389     0.6603 0.724 0.084 0.072 0.120
#&gt; SRR1946647     2  0.4304     0.7321 0.284 0.716 0.000 0.000
#&gt; SRR1946646     3  0.1356     0.7820 0.008 0.000 0.960 0.032
#&gt; SRR1946645     1  0.0707     0.8057 0.980 0.020 0.000 0.000
#&gt; SRR1946644     3  0.0336     0.7990 0.000 0.008 0.992 0.000
#&gt; SRR1946643     3  0.3610     0.6724 0.000 0.000 0.800 0.200
#&gt; SRR1946642     1  0.0000     0.8136 1.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.8136 1.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.4103     0.6111 0.000 0.000 0.744 0.256
#&gt; SRR1946640     1  0.0000     0.8136 1.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.8136 1.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.8136 1.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.8136 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.2329     0.6855 0.000 0.000 0.876 0.000 0.124
#&gt; SRR1946691     2  0.4297     0.0657 0.000 0.528 0.000 0.472 0.000
#&gt; SRR1946690     2  0.1121     0.8304 0.000 0.956 0.000 0.044 0.000
#&gt; SRR1946689     4  0.2020     0.7201 0.000 0.000 0.100 0.900 0.000
#&gt; SRR1946686     3  0.3895     0.5002 0.320 0.000 0.680 0.000 0.000
#&gt; SRR1946685     2  0.0963     0.8538 0.000 0.964 0.036 0.000 0.000
#&gt; SRR1946688     4  0.1544     0.7006 0.000 0.068 0.000 0.932 0.000
#&gt; SRR1946684     5  0.0000     0.8670 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946683     5  0.0000     0.8670 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946682     5  0.2864     0.8002 0.000 0.012 0.000 0.136 0.852
#&gt; SRR1946680     4  0.4045     0.5313 0.000 0.000 0.356 0.644 0.000
#&gt; SRR1946681     3  0.4192     0.3073 0.000 0.404 0.596 0.000 0.000
#&gt; SRR1946687     4  0.5594     0.3790 0.064 0.000 0.400 0.532 0.004
#&gt; SRR1946679     2  0.1121     0.8502 0.000 0.956 0.044 0.000 0.000
#&gt; SRR1946678     1  0.2424     0.8077 0.868 0.000 0.000 0.000 0.132
#&gt; SRR1946676     2  0.1792     0.8234 0.000 0.916 0.084 0.000 0.000
#&gt; SRR1946677     5  0.0000     0.8670 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946672     3  0.2189     0.7159 0.084 0.012 0.904 0.000 0.000
#&gt; SRR1946673     5  0.0000     0.8670 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946671     5  0.5941     0.4757 0.168 0.244 0.000 0.000 0.588
#&gt; SRR1946669     5  0.0162     0.8659 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1946668     5  0.0566     0.8641 0.004 0.000 0.000 0.012 0.984
#&gt; SRR1946666     1  0.3242     0.6691 0.784 0.000 0.216 0.000 0.000
#&gt; SRR1946667     4  0.2020     0.7201 0.000 0.000 0.100 0.900 0.000
#&gt; SRR1946670     4  0.3141     0.6357 0.000 0.016 0.000 0.832 0.152
#&gt; SRR1946663     5  0.2890     0.7888 0.000 0.004 0.000 0.160 0.836
#&gt; SRR1946664     2  0.0290     0.8505 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1946662     5  0.0000     0.8670 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946661     5  0.3911     0.7782 0.004 0.084 0.000 0.100 0.812
#&gt; SRR1946660     4  0.3837     0.3972 0.000 0.308 0.000 0.692 0.000
#&gt; SRR1946659     1  0.0000     0.9467 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946658     5  0.5130     0.6241 0.000 0.220 0.000 0.100 0.680
#&gt; SRR1946657     2  0.0880     0.8545 0.000 0.968 0.032 0.000 0.000
#&gt; SRR1946655     3  0.0290     0.7034 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1946654     3  0.1704     0.7289 0.004 0.068 0.928 0.000 0.000
#&gt; SRR1946653     3  0.6417     0.1416 0.228 0.000 0.508 0.264 0.000
#&gt; SRR1946652     5  0.2471     0.7841 0.000 0.136 0.000 0.000 0.864
#&gt; SRR1946651     2  0.0290     0.8555 0.000 0.992 0.008 0.000 0.000
#&gt; SRR1946650     2  0.5158     0.5382 0.000 0.676 0.000 0.100 0.224
#&gt; SRR1946649     2  0.4010     0.7129 0.088 0.796 0.000 0.000 0.116
#&gt; SRR1946648     3  0.4060     0.4579 0.000 0.000 0.640 0.000 0.360
#&gt; SRR1946647     5  0.0000     0.8670 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946646     2  0.2685     0.8028 0.092 0.880 0.028 0.000 0.000
#&gt; SRR1946645     5  0.3895     0.5366 0.320 0.000 0.000 0.000 0.680
#&gt; SRR1946644     2  0.0290     0.8555 0.000 0.992 0.008 0.000 0.000
#&gt; SRR1946643     3  0.2020     0.7255 0.000 0.100 0.900 0.000 0.000
#&gt; SRR1946642     1  0.0000     0.9467 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.9467 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.1965     0.7267 0.000 0.096 0.904 0.000 0.000
#&gt; SRR1946640     1  0.0000     0.9467 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.9467 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9467 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9467 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.1080      0.779 0.000 0.000 0.960 0.004 0.032 0.004
#&gt; SRR1946691     2  0.6679      0.149 0.000 0.452 0.004 0.208 0.040 0.296
#&gt; SRR1946690     2  0.0291      0.857 0.000 0.992 0.004 0.000 0.000 0.004
#&gt; SRR1946689     4  0.0363      0.719 0.000 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1946686     3  0.2805      0.643 0.160 0.000 0.828 0.000 0.012 0.000
#&gt; SRR1946685     2  0.0260      0.856 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1946688     6  0.4265      0.487 0.000 0.004 0.004 0.236 0.044 0.712
#&gt; SRR1946684     5  0.0713      0.745 0.000 0.000 0.000 0.000 0.972 0.028
#&gt; SRR1946683     6  0.5065      0.245 0.000 0.000 0.080 0.000 0.396 0.524
#&gt; SRR1946682     6  0.2812      0.635 0.000 0.000 0.000 0.048 0.096 0.856
#&gt; SRR1946680     4  0.2340      0.710 0.000 0.000 0.148 0.852 0.000 0.000
#&gt; SRR1946681     3  0.4172      0.205 0.000 0.424 0.564 0.000 0.004 0.008
#&gt; SRR1946687     4  0.5137      0.600 0.136 0.000 0.228 0.632 0.004 0.000
#&gt; SRR1946679     2  0.0653      0.853 0.000 0.980 0.004 0.000 0.004 0.012
#&gt; SRR1946678     5  0.4026      0.364 0.376 0.000 0.000 0.000 0.612 0.012
#&gt; SRR1946676     2  0.5228      0.129 0.000 0.524 0.100 0.000 0.000 0.376
#&gt; SRR1946677     6  0.3566      0.585 0.000 0.000 0.020 0.000 0.236 0.744
#&gt; SRR1946672     3  0.0547      0.786 0.020 0.000 0.980 0.000 0.000 0.000
#&gt; SRR1946673     5  0.1204      0.741 0.000 0.000 0.000 0.000 0.944 0.056
#&gt; SRR1946671     6  0.5198      0.587 0.064 0.032 0.016 0.000 0.200 0.688
#&gt; SRR1946669     5  0.1471      0.738 0.004 0.000 0.000 0.000 0.932 0.064
#&gt; SRR1946668     5  0.0603      0.737 0.004 0.000 0.000 0.000 0.980 0.016
#&gt; SRR1946666     1  0.4274      0.423 0.640 0.000 0.336 0.008 0.004 0.012
#&gt; SRR1946667     4  0.0260      0.720 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1946670     5  0.5869      0.264 0.000 0.000 0.004 0.208 0.504 0.284
#&gt; SRR1946663     6  0.3575      0.607 0.000 0.000 0.000 0.128 0.076 0.796
#&gt; SRR1946664     2  0.0405      0.855 0.000 0.988 0.004 0.000 0.000 0.008
#&gt; SRR1946662     5  0.1531      0.736 0.004 0.000 0.000 0.000 0.928 0.068
#&gt; SRR1946661     6  0.1531      0.660 0.000 0.004 0.000 0.000 0.068 0.928
#&gt; SRR1946660     6  0.4157      0.593 0.000 0.032 0.004 0.104 0.072 0.788
#&gt; SRR1946659     1  0.0146      0.931 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1946658     5  0.4048      0.461 0.000 0.012 0.012 0.000 0.684 0.292
#&gt; SRR1946657     2  0.0000      0.857 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946655     3  0.0458      0.786 0.000 0.000 0.984 0.016 0.000 0.000
#&gt; SRR1946654     3  0.0810      0.786 0.000 0.004 0.976 0.008 0.004 0.008
#&gt; SRR1946653     4  0.6670      0.192 0.136 0.000 0.392 0.408 0.004 0.060
#&gt; SRR1946652     5  0.5700      0.220 0.000 0.152 0.008 0.000 0.536 0.304
#&gt; SRR1946651     2  0.0547      0.851 0.000 0.980 0.000 0.000 0.000 0.020
#&gt; SRR1946650     6  0.3798      0.604 0.000 0.216 0.004 0.000 0.032 0.748
#&gt; SRR1946649     6  0.5194      0.588 0.044 0.208 0.012 0.000 0.052 0.684
#&gt; SRR1946648     3  0.5488      0.268 0.000 0.000 0.556 0.000 0.272 0.172
#&gt; SRR1946647     5  0.0146      0.743 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1946646     2  0.1387      0.809 0.068 0.932 0.000 0.000 0.000 0.000
#&gt; SRR1946645     6  0.4891      0.590 0.140 0.000 0.016 0.000 0.148 0.696
#&gt; SRR1946644     2  0.0000      0.857 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946643     3  0.0458      0.789 0.000 0.016 0.984 0.000 0.000 0.000
#&gt; SRR1946642     1  0.0146      0.931 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1946641     1  0.0000      0.934 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0603      0.788 0.000 0.016 0.980 0.004 0.000 0.000
#&gt; SRR1946640     1  0.0000      0.934 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.934 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.934 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.934 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.562           0.729       0.840          0.235 0.795   0.795
#> 3 3 0.591           0.133       0.615          0.613 0.522   0.452
#> 4 4 0.600           0.707       0.850          0.233 0.578   0.386
#> 5 5 0.512           0.295       0.648          0.343 0.546   0.279
#> 6 6 0.544           0.685       0.765          0.121 0.739   0.400
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1  0.8813     0.4220 0.700 0.300
#&gt; SRR1946691     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946690     1  0.2603     0.8232 0.956 0.044
#&gt; SRR1946689     2  0.0000     0.5808 0.000 1.000
#&gt; SRR1946686     1  0.8861     0.4108 0.696 0.304
#&gt; SRR1946685     1  0.0376     0.8675 0.996 0.004
#&gt; SRR1946688     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946684     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946683     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946682     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946680     2  0.9795     0.6224 0.416 0.584
#&gt; SRR1946681     1  0.8763     0.3197 0.704 0.296
#&gt; SRR1946687     1  0.8813     0.4220 0.700 0.300
#&gt; SRR1946679     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946678     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946676     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946677     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946672     1  0.9661     0.0691 0.608 0.392
#&gt; SRR1946673     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946671     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946669     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946668     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946666     1  0.8813     0.4220 0.700 0.300
#&gt; SRR1946667     2  0.0000     0.5808 0.000 1.000
#&gt; SRR1946670     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946663     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946664     1  0.2603     0.8232 0.956 0.044
#&gt; SRR1946662     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946661     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946660     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946659     1  0.8813     0.4220 0.700 0.300
#&gt; SRR1946658     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946657     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946655     2  0.9815     0.6200 0.420 0.580
#&gt; SRR1946654     1  0.8861     0.4108 0.696 0.304
#&gt; SRR1946653     1  0.8813     0.4220 0.700 0.300
#&gt; SRR1946652     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946651     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946650     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946649     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946648     1  0.8763     0.4312 0.704 0.296
#&gt; SRR1946647     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946646     1  0.8813     0.4220 0.700 0.300
#&gt; SRR1946645     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946644     1  0.8763     0.4307 0.704 0.296
#&gt; SRR1946643     2  0.9815     0.6200 0.420 0.580
#&gt; SRR1946642     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946641     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946656     2  0.9815     0.6200 0.420 0.580
#&gt; SRR1946640     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946639     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946638     1  0.0000     0.8709 1.000 0.000
#&gt; SRR1946637     1  0.0000     0.8709 1.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     1  0.0000      0.313 1.000 0.000 0.000
#&gt; SRR1946691     2  0.6816      0.778 0.472 0.516 0.012
#&gt; SRR1946690     2  0.6984      0.476 0.420 0.560 0.020
#&gt; SRR1946689     3  0.0892      1.000 0.020 0.000 0.980
#&gt; SRR1946686     1  0.0424      0.313 0.992 0.008 0.000
#&gt; SRR1946685     1  0.6305     -0.781 0.516 0.484 0.000
#&gt; SRR1946688     2  0.6816      0.778 0.472 0.516 0.012
#&gt; SRR1946684     1  0.6309     -0.809 0.500 0.500 0.000
#&gt; SRR1946683     1  0.6309     -0.809 0.500 0.500 0.000
#&gt; SRR1946682     2  0.6302      0.799 0.480 0.520 0.000
#&gt; SRR1946680     1  0.7487     -0.313 0.500 0.464 0.036
#&gt; SRR1946681     2  0.5098     -0.248 0.248 0.752 0.000
#&gt; SRR1946687     1  0.0000      0.313 1.000 0.000 0.000
#&gt; SRR1946679     2  0.6307      0.802 0.488 0.512 0.000
#&gt; SRR1946678     2  0.6309      0.792 0.500 0.500 0.000
#&gt; SRR1946676     2  0.6307      0.802 0.488 0.512 0.000
#&gt; SRR1946677     2  0.6302      0.799 0.480 0.520 0.000
#&gt; SRR1946672     1  0.4978      0.168 0.780 0.216 0.004
#&gt; SRR1946673     1  0.6309     -0.809 0.500 0.500 0.000
#&gt; SRR1946671     1  0.6309     -0.809 0.500 0.500 0.000
#&gt; SRR1946669     2  0.6309      0.792 0.500 0.500 0.000
#&gt; SRR1946668     1  0.6309     -0.809 0.500 0.500 0.000
#&gt; SRR1946666     1  0.0000      0.313 1.000 0.000 0.000
#&gt; SRR1946667     3  0.0892      1.000 0.020 0.000 0.980
#&gt; SRR1946670     2  0.6308      0.801 0.492 0.508 0.000
#&gt; SRR1946663     2  0.6302      0.799 0.480 0.520 0.000
#&gt; SRR1946664     2  0.6984      0.476 0.420 0.560 0.020
#&gt; SRR1946662     2  0.6309      0.792 0.500 0.500 0.000
#&gt; SRR1946661     2  0.6307      0.799 0.488 0.512 0.000
#&gt; SRR1946660     2  0.6816      0.778 0.472 0.516 0.012
#&gt; SRR1946659     1  0.0000      0.313 1.000 0.000 0.000
#&gt; SRR1946658     2  0.6307      0.802 0.488 0.512 0.000
#&gt; SRR1946657     1  0.6307     -0.787 0.512 0.488 0.000
#&gt; SRR1946655     1  0.7286     -0.306 0.508 0.464 0.028
#&gt; SRR1946654     1  0.0237      0.313 0.996 0.004 0.000
#&gt; SRR1946653     1  0.0000      0.313 1.000 0.000 0.000
#&gt; SRR1946652     2  0.6308      0.801 0.492 0.508 0.000
#&gt; SRR1946651     2  0.6307      0.802 0.488 0.512 0.000
#&gt; SRR1946650     2  0.6302      0.799 0.480 0.520 0.000
#&gt; SRR1946649     1  0.6309     -0.809 0.500 0.500 0.000
#&gt; SRR1946648     1  0.0424      0.309 0.992 0.008 0.000
#&gt; SRR1946647     1  0.6309     -0.809 0.500 0.500 0.000
#&gt; SRR1946646     1  0.0592      0.310 0.988 0.012 0.000
#&gt; SRR1946645     1  0.6307     -0.798 0.512 0.488 0.000
#&gt; SRR1946644     1  0.0747      0.307 0.984 0.016 0.000
#&gt; SRR1946643     1  0.7286     -0.306 0.508 0.464 0.028
#&gt; SRR1946642     2  0.6309      0.792 0.500 0.500 0.000
#&gt; SRR1946641     1  0.6307     -0.798 0.512 0.488 0.000
#&gt; SRR1946656     1  0.7286     -0.306 0.508 0.464 0.028
#&gt; SRR1946640     1  0.6307     -0.798 0.512 0.488 0.000
#&gt; SRR1946639     1  0.6307     -0.798 0.512 0.488 0.000
#&gt; SRR1946638     1  0.6307     -0.798 0.512 0.488 0.000
#&gt; SRR1946637     1  0.6307     -0.798 0.512 0.488 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.4999      0.614 0.000 0.492 0.508 0.000
#&gt; SRR1946691     2  0.5366      0.270 0.440 0.548 0.012 0.000
#&gt; SRR1946690     1  0.0592      1.000 0.984 0.016 0.000 0.000
#&gt; SRR1946689     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1946686     3  0.4999      0.616 0.000 0.492 0.508 0.000
#&gt; SRR1946685     2  0.1520      0.868 0.020 0.956 0.024 0.000
#&gt; SRR1946688     2  0.5366      0.270 0.440 0.548 0.012 0.000
#&gt; SRR1946684     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946683     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946682     2  0.2402      0.833 0.076 0.912 0.012 0.000
#&gt; SRR1946680     3  0.1394      0.222 0.008 0.012 0.964 0.016
#&gt; SRR1946681     3  0.5389      0.126 0.032 0.308 0.660 0.000
#&gt; SRR1946687     3  0.4999      0.614 0.000 0.492 0.508 0.000
#&gt; SRR1946679     2  0.1209      0.877 0.032 0.964 0.004 0.000
#&gt; SRR1946678     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946676     2  0.1209      0.877 0.032 0.964 0.004 0.000
#&gt; SRR1946677     2  0.2402      0.833 0.076 0.912 0.012 0.000
#&gt; SRR1946672     3  0.4428      0.557 0.000 0.276 0.720 0.004
#&gt; SRR1946673     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946671     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946669     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946668     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946666     3  0.4999      0.614 0.000 0.492 0.508 0.000
#&gt; SRR1946667     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1946670     2  0.1022      0.878 0.032 0.968 0.000 0.000
#&gt; SRR1946663     2  0.2402      0.833 0.076 0.912 0.012 0.000
#&gt; SRR1946664     1  0.0592      1.000 0.984 0.016 0.000 0.000
#&gt; SRR1946662     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946661     2  0.1284      0.871 0.024 0.964 0.012 0.000
#&gt; SRR1946660     2  0.5366      0.270 0.440 0.548 0.012 0.000
#&gt; SRR1946659     3  0.4999      0.614 0.000 0.492 0.508 0.000
#&gt; SRR1946658     2  0.1209      0.877 0.032 0.964 0.004 0.000
#&gt; SRR1946657     2  0.1411      0.872 0.020 0.960 0.020 0.000
#&gt; SRR1946655     3  0.1139      0.232 0.008 0.012 0.972 0.008
#&gt; SRR1946654     3  0.4996      0.618 0.000 0.484 0.516 0.000
#&gt; SRR1946653     3  0.4999      0.614 0.000 0.492 0.508 0.000
#&gt; SRR1946652     2  0.0921      0.879 0.028 0.972 0.000 0.000
#&gt; SRR1946651     2  0.1209      0.877 0.032 0.964 0.004 0.000
#&gt; SRR1946650     2  0.2542      0.825 0.084 0.904 0.012 0.000
#&gt; SRR1946649     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946648     2  0.5000     -0.642 0.000 0.500 0.500 0.000
#&gt; SRR1946647     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946646     3  0.5168      0.609 0.004 0.492 0.504 0.000
#&gt; SRR1946645     2  0.1297      0.879 0.020 0.964 0.016 0.000
#&gt; SRR1946644     3  0.5168      0.602 0.004 0.496 0.500 0.000
#&gt; SRR1946643     3  0.1139      0.232 0.008 0.012 0.972 0.008
#&gt; SRR1946642     2  0.0000      0.884 0.000 1.000 0.000 0.000
#&gt; SRR1946641     2  0.0707      0.876 0.000 0.980 0.020 0.000
#&gt; SRR1946656     3  0.1139      0.232 0.008 0.012 0.972 0.008
#&gt; SRR1946640     2  0.0707      0.876 0.000 0.980 0.020 0.000
#&gt; SRR1946639     2  0.0707      0.876 0.000 0.980 0.020 0.000
#&gt; SRR1946638     2  0.0707      0.876 0.000 0.980 0.020 0.000
#&gt; SRR1946637     2  0.0707      0.876 0.000 0.980 0.020 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.0162     0.4522 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1946691     2  0.4313     0.4387 0.356 0.636 0.008 0.000 0.000
#&gt; SRR1946690     1  0.0290     1.0000 0.992 0.008 0.000 0.000 0.000
#&gt; SRR1946689     4  0.0000     1.0000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946686     3  0.0162     0.4506 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1946685     3  0.6469     0.3047 0.000 0.336 0.468 0.000 0.196
#&gt; SRR1946688     2  0.4313     0.4387 0.356 0.636 0.008 0.000 0.000
#&gt; SRR1946684     5  0.5546     0.2043 0.000 0.068 0.436 0.000 0.496
#&gt; SRR1946683     5  0.5399     0.2300 0.000 0.056 0.448 0.000 0.496
#&gt; SRR1946682     2  0.1670     0.6827 0.000 0.936 0.052 0.000 0.012
#&gt; SRR1946680     5  0.4815    -0.1848 0.008 0.000 0.480 0.008 0.504
#&gt; SRR1946681     5  0.6522    -0.3262 0.000 0.300 0.224 0.000 0.476
#&gt; SRR1946687     3  0.0290     0.4518 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1946679     3  0.6585     0.2968 0.000 0.360 0.428 0.000 0.212
#&gt; SRR1946678     5  0.5399     0.2300 0.000 0.056 0.448 0.000 0.496
#&gt; SRR1946676     3  0.6585     0.2968 0.000 0.360 0.428 0.000 0.212
#&gt; SRR1946677     2  0.1670     0.6827 0.000 0.936 0.052 0.000 0.012
#&gt; SRR1946672     3  0.3395     0.1880 0.000 0.000 0.764 0.000 0.236
#&gt; SRR1946673     5  0.5546     0.2043 0.000 0.068 0.436 0.000 0.496
#&gt; SRR1946671     5  0.5399     0.2300 0.000 0.056 0.448 0.000 0.496
#&gt; SRR1946669     5  0.5450     0.2063 0.000 0.060 0.444 0.000 0.496
#&gt; SRR1946668     5  0.5399     0.2300 0.000 0.056 0.448 0.000 0.496
#&gt; SRR1946666     3  0.0290     0.4518 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1946667     4  0.0000     1.0000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946670     3  0.6589     0.2864 0.000 0.364 0.424 0.000 0.212
#&gt; SRR1946663     2  0.1670     0.6827 0.000 0.936 0.052 0.000 0.012
#&gt; SRR1946664     1  0.0290     1.0000 0.992 0.008 0.000 0.000 0.000
#&gt; SRR1946662     5  0.5546     0.2043 0.000 0.068 0.436 0.000 0.496
#&gt; SRR1946661     5  0.6710     0.0779 0.008 0.236 0.264 0.000 0.492
#&gt; SRR1946660     2  0.4313     0.4387 0.356 0.636 0.008 0.000 0.000
#&gt; SRR1946659     3  0.0290     0.4518 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1946658     3  0.6600     0.2862 0.000 0.380 0.408 0.000 0.212
#&gt; SRR1946657     3  0.6511     0.2997 0.000 0.336 0.460 0.000 0.204
#&gt; SRR1946655     5  0.4561    -0.1782 0.008 0.000 0.488 0.000 0.504
#&gt; SRR1946654     3  0.0451     0.4474 0.000 0.004 0.988 0.000 0.008
#&gt; SRR1946653     3  0.0290     0.4518 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1946652     3  0.6534     0.2869 0.000 0.328 0.460 0.000 0.212
#&gt; SRR1946651     3  0.6585     0.2968 0.000 0.360 0.428 0.000 0.212
#&gt; SRR1946650     2  0.1883     0.6794 0.008 0.932 0.048 0.000 0.012
#&gt; SRR1946649     5  0.5399     0.2300 0.000 0.056 0.448 0.000 0.496
#&gt; SRR1946648     3  0.0162     0.4514 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1946647     5  0.5399     0.2300 0.000 0.056 0.448 0.000 0.496
#&gt; SRR1946646     3  0.1041     0.4408 0.000 0.032 0.964 0.000 0.004
#&gt; SRR1946645     2  0.5401    -0.1509 0.000 0.536 0.404 0.000 0.060
#&gt; SRR1946644     3  0.1281     0.4410 0.000 0.032 0.956 0.000 0.012
#&gt; SRR1946643     5  0.4561    -0.1782 0.008 0.000 0.488 0.000 0.504
#&gt; SRR1946642     5  0.5399     0.2300 0.000 0.056 0.448 0.000 0.496
#&gt; SRR1946641     3  0.4561    -0.1510 0.000 0.008 0.504 0.000 0.488
#&gt; SRR1946656     5  0.4561    -0.1782 0.008 0.000 0.488 0.000 0.504
#&gt; SRR1946640     3  0.4561    -0.1510 0.000 0.008 0.504 0.000 0.488
#&gt; SRR1946639     3  0.4561    -0.1510 0.000 0.008 0.504 0.000 0.488
#&gt; SRR1946638     3  0.4561    -0.1510 0.000 0.008 0.504 0.000 0.488
#&gt; SRR1946637     3  0.4561    -0.1510 0.000 0.008 0.504 0.000 0.488
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.2527      0.936 0.000 0.000 0.832 0.000 0.168 0.000
#&gt; SRR1946691     6  0.0363      0.473 0.000 0.000 0.000 0.000 0.012 0.988
#&gt; SRR1946690     2  0.5036      1.000 0.000 0.632 0.140 0.000 0.000 0.228
#&gt; SRR1946689     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946686     3  0.2668      0.935 0.004 0.000 0.828 0.000 0.168 0.000
#&gt; SRR1946685     5  0.3052      0.406 0.000 0.004 0.216 0.000 0.780 0.000
#&gt; SRR1946688     6  0.0363      0.473 0.000 0.000 0.000 0.000 0.012 0.988
#&gt; SRR1946684     5  0.5568      0.703 0.288 0.020 0.088 0.000 0.596 0.008
#&gt; SRR1946683     5  0.6250      0.698 0.288 0.024 0.136 0.000 0.536 0.016
#&gt; SRR1946682     6  0.5126      0.674 0.000 0.364 0.056 0.000 0.016 0.564
#&gt; SRR1946680     1  0.3910      0.824 0.660 0.000 0.328 0.008 0.000 0.004
#&gt; SRR1946681     1  0.3950      0.377 0.672 0.000 0.008 0.000 0.312 0.008
#&gt; SRR1946687     3  0.2491      0.937 0.000 0.000 0.836 0.000 0.164 0.000
#&gt; SRR1946679     5  0.0551      0.521 0.000 0.004 0.004 0.000 0.984 0.008
#&gt; SRR1946678     5  0.6154      0.703 0.288 0.024 0.124 0.000 0.548 0.016
#&gt; SRR1946676     5  0.0551      0.521 0.000 0.004 0.004 0.000 0.984 0.008
#&gt; SRR1946677     6  0.5177      0.673 0.000 0.364 0.060 0.000 0.016 0.560
#&gt; SRR1946672     3  0.3592      0.375 0.240 0.000 0.740 0.000 0.020 0.000
#&gt; SRR1946673     5  0.5568      0.703 0.288 0.020 0.088 0.000 0.596 0.008
#&gt; SRR1946671     5  0.6445      0.683 0.288 0.024 0.164 0.000 0.508 0.016
#&gt; SRR1946669     5  0.5651      0.704 0.288 0.020 0.096 0.000 0.588 0.008
#&gt; SRR1946668     5  0.6154      0.703 0.288 0.024 0.124 0.000 0.548 0.016
#&gt; SRR1946666     3  0.2491      0.937 0.000 0.000 0.836 0.000 0.164 0.000
#&gt; SRR1946667     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946670     5  0.1716      0.520 0.000 0.004 0.028 0.000 0.932 0.036
#&gt; SRR1946663     6  0.5126      0.674 0.000 0.364 0.056 0.000 0.016 0.564
#&gt; SRR1946664     2  0.5036      1.000 0.000 0.632 0.140 0.000 0.000 0.228
#&gt; SRR1946662     5  0.5568      0.703 0.288 0.020 0.088 0.000 0.596 0.008
#&gt; SRR1946661     5  0.8032      0.539 0.288 0.164 0.108 0.000 0.376 0.064
#&gt; SRR1946660     6  0.0363      0.473 0.000 0.000 0.000 0.000 0.012 0.988
#&gt; SRR1946659     3  0.2491      0.937 0.000 0.000 0.836 0.000 0.164 0.000
#&gt; SRR1946658     5  0.1155      0.503 0.000 0.004 0.004 0.000 0.956 0.036
#&gt; SRR1946657     5  0.3043      0.435 0.004 0.004 0.196 0.000 0.796 0.000
#&gt; SRR1946655     1  0.3351      0.853 0.712 0.000 0.288 0.000 0.000 0.000
#&gt; SRR1946654     3  0.2706      0.933 0.008 0.000 0.832 0.000 0.160 0.000
#&gt; SRR1946653     3  0.2491      0.937 0.000 0.000 0.836 0.000 0.164 0.000
#&gt; SRR1946652     5  0.1477      0.540 0.000 0.004 0.048 0.000 0.940 0.008
#&gt; SRR1946651     5  0.0551      0.521 0.000 0.004 0.004 0.000 0.984 0.008
#&gt; SRR1946650     6  0.4991      0.672 0.000 0.364 0.052 0.000 0.012 0.572
#&gt; SRR1946649     5  0.6445      0.683 0.288 0.024 0.164 0.000 0.508 0.016
#&gt; SRR1946648     3  0.2703      0.932 0.004 0.000 0.824 0.000 0.172 0.000
#&gt; SRR1946647     5  0.6154      0.703 0.288 0.024 0.124 0.000 0.548 0.016
#&gt; SRR1946646     3  0.2883      0.899 0.000 0.000 0.788 0.000 0.212 0.000
#&gt; SRR1946645     6  0.7941      0.112 0.020 0.188 0.276 0.000 0.180 0.336
#&gt; SRR1946644     3  0.3136      0.885 0.004 0.000 0.768 0.000 0.228 0.000
#&gt; SRR1946643     1  0.3351      0.853 0.712 0.000 0.288 0.000 0.000 0.000
#&gt; SRR1946642     5  0.6154      0.703 0.288 0.024 0.124 0.000 0.548 0.016
#&gt; SRR1946641     5  0.6104      0.496 0.288 0.000 0.348 0.000 0.364 0.000
#&gt; SRR1946656     1  0.3351      0.853 0.712 0.000 0.288 0.000 0.000 0.000
#&gt; SRR1946640     5  0.6104      0.496 0.288 0.000 0.348 0.000 0.364 0.000
#&gt; SRR1946639     5  0.6104      0.496 0.288 0.000 0.348 0.000 0.364 0.000
#&gt; SRR1946638     5  0.6104      0.496 0.288 0.000 0.348 0.000 0.364 0.000
#&gt; SRR1946637     5  0.6104      0.496 0.288 0.000 0.348 0.000 0.364 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.220           0.651       0.822         0.4219 0.570   0.570
#> 3 3 0.323           0.468       0.693         0.4255 0.577   0.386
#> 4 4 0.448           0.556       0.712         0.1486 0.838   0.621
#> 5 5 0.491           0.495       0.585         0.0861 0.790   0.413
#> 6 6 0.529           0.474       0.593         0.0606 0.852   0.443
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.9754      0.668 0.408 0.592
#&gt; SRR1946691     1  0.9248      0.570 0.660 0.340
#&gt; SRR1946690     2  0.9983     -0.230 0.476 0.524
#&gt; SRR1946689     2  0.1414      0.619 0.020 0.980
#&gt; SRR1946686     1  0.6623      0.590 0.828 0.172
#&gt; SRR1946685     1  0.0376      0.797 0.996 0.004
#&gt; SRR1946688     2  0.9998     -0.252 0.492 0.508
#&gt; SRR1946684     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946683     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946682     1  0.6801      0.722 0.820 0.180
#&gt; SRR1946680     2  0.4815      0.683 0.104 0.896
#&gt; SRR1946681     1  0.9922      0.215 0.552 0.448
#&gt; SRR1946687     2  0.9608      0.697 0.384 0.616
#&gt; SRR1946679     1  0.6247      0.737 0.844 0.156
#&gt; SRR1946678     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946676     1  0.5946      0.740 0.856 0.144
#&gt; SRR1946677     1  0.5737      0.751 0.864 0.136
#&gt; SRR1946672     2  0.8267      0.741 0.260 0.740
#&gt; SRR1946673     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946671     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946669     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946668     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946666     2  0.9754      0.668 0.408 0.592
#&gt; SRR1946667     2  0.1414      0.619 0.020 0.980
#&gt; SRR1946670     1  0.7674      0.698 0.776 0.224
#&gt; SRR1946663     1  0.6887      0.719 0.816 0.184
#&gt; SRR1946664     1  0.9393      0.553 0.644 0.356
#&gt; SRR1946662     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946661     1  0.6712      0.725 0.824 0.176
#&gt; SRR1946660     1  0.9248      0.570 0.660 0.340
#&gt; SRR1946659     2  0.9608      0.697 0.384 0.616
#&gt; SRR1946658     1  0.9044      0.600 0.680 0.320
#&gt; SRR1946657     1  0.3879      0.783 0.924 0.076
#&gt; SRR1946655     2  0.7528      0.739 0.216 0.784
#&gt; SRR1946654     2  0.9129      0.730 0.328 0.672
#&gt; SRR1946653     2  0.9427      0.716 0.360 0.640
#&gt; SRR1946652     1  0.2603      0.795 0.956 0.044
#&gt; SRR1946651     1  0.7139      0.714 0.804 0.196
#&gt; SRR1946650     1  0.6973      0.717 0.812 0.188
#&gt; SRR1946649     1  0.1633      0.796 0.976 0.024
#&gt; SRR1946648     1  0.9963     -0.439 0.536 0.464
#&gt; SRR1946647     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946646     2  0.9170      0.727 0.332 0.668
#&gt; SRR1946645     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946644     1  0.3584      0.786 0.932 0.068
#&gt; SRR1946643     2  0.7528      0.739 0.216 0.784
#&gt; SRR1946642     1  0.0000      0.798 1.000 0.000
#&gt; SRR1946641     1  0.5178      0.683 0.884 0.116
#&gt; SRR1946656     2  0.7528      0.739 0.216 0.784
#&gt; SRR1946640     1  0.6247      0.619 0.844 0.156
#&gt; SRR1946639     1  0.4298      0.719 0.912 0.088
#&gt; SRR1946638     1  0.6247      0.619 0.844 0.156
#&gt; SRR1946637     1  0.6247      0.619 0.844 0.156
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     1   0.653     -0.260 0.588 0.008 0.404
#&gt; SRR1946691     2   0.445      0.680 0.000 0.808 0.192
#&gt; SRR1946690     2   0.470      0.674 0.000 0.788 0.212
#&gt; SRR1946689     3   0.346      0.636 0.012 0.096 0.892
#&gt; SRR1946686     1   0.258      0.514 0.928 0.064 0.008
#&gt; SRR1946685     2   0.583      0.365 0.340 0.660 0.000
#&gt; SRR1946688     2   0.486      0.671 0.008 0.800 0.192
#&gt; SRR1946684     1   0.581      0.450 0.664 0.336 0.000
#&gt; SRR1946683     1   0.631      0.109 0.504 0.496 0.000
#&gt; SRR1946682     2   0.263      0.762 0.084 0.916 0.000
#&gt; SRR1946680     3   0.591      0.735 0.144 0.068 0.788
#&gt; SRR1946681     2   0.765      0.553 0.124 0.680 0.196
#&gt; SRR1946687     1   0.654     -0.266 0.584 0.008 0.408
#&gt; SRR1946679     2   0.477      0.751 0.100 0.848 0.052
#&gt; SRR1946678     1   0.546      0.488 0.712 0.288 0.000
#&gt; SRR1946676     2   0.492      0.745 0.108 0.840 0.052
#&gt; SRR1946677     2   0.280      0.759 0.092 0.908 0.000
#&gt; SRR1946672     3   0.776      0.720 0.360 0.060 0.580
#&gt; SRR1946673     1   0.583      0.445 0.660 0.340 0.000
#&gt; SRR1946671     1   0.630      0.169 0.524 0.476 0.000
#&gt; SRR1946669     1   0.581      0.450 0.664 0.336 0.000
#&gt; SRR1946668     1   0.581      0.450 0.664 0.336 0.000
#&gt; SRR1946666     1   0.654     -0.262 0.584 0.008 0.408
#&gt; SRR1946667     3   0.346      0.636 0.012 0.096 0.892
#&gt; SRR1946670     2   0.183      0.777 0.036 0.956 0.008
#&gt; SRR1946663     2   0.254      0.763 0.080 0.920 0.000
#&gt; SRR1946664     2   0.460      0.679 0.000 0.796 0.204
#&gt; SRR1946662     1   0.583      0.445 0.660 0.340 0.000
#&gt; SRR1946661     2   0.263      0.763 0.084 0.916 0.000
#&gt; SRR1946660     2   0.445      0.680 0.000 0.808 0.192
#&gt; SRR1946659     1   0.634     -0.250 0.596 0.004 0.400
#&gt; SRR1946658     2   0.192      0.772 0.020 0.956 0.024
#&gt; SRR1946657     2   0.447      0.697 0.164 0.828 0.008
#&gt; SRR1946655     3   0.783      0.771 0.312 0.076 0.612
#&gt; SRR1946654     1   0.802     -0.410 0.520 0.064 0.416
#&gt; SRR1946653     1   0.707     -0.303 0.568 0.024 0.408
#&gt; SRR1946652     2   0.412      0.705 0.168 0.832 0.000
#&gt; SRR1946651     2   0.469      0.753 0.096 0.852 0.052
#&gt; SRR1946650     2   0.153      0.775 0.040 0.960 0.000
#&gt; SRR1946649     2   0.562      0.474 0.308 0.692 0.000
#&gt; SRR1946648     1   0.821      0.130 0.600 0.104 0.296
#&gt; SRR1946647     1   0.581      0.450 0.664 0.336 0.000
#&gt; SRR1946646     1   0.813     -0.382 0.528 0.072 0.400
#&gt; SRR1946645     1   0.630      0.143 0.516 0.484 0.000
#&gt; SRR1946644     2   0.534      0.613 0.232 0.760 0.008
#&gt; SRR1946643     3   0.783      0.771 0.312 0.076 0.612
#&gt; SRR1946642     1   0.616      0.486 0.696 0.288 0.016
#&gt; SRR1946641     1   0.375      0.549 0.884 0.096 0.020
#&gt; SRR1946656     3   0.783      0.771 0.312 0.076 0.612
#&gt; SRR1946640     1   0.375      0.549 0.884 0.096 0.020
#&gt; SRR1946639     1   0.383      0.551 0.880 0.100 0.020
#&gt; SRR1946638     1   0.375      0.549 0.884 0.096 0.020
#&gt; SRR1946637     1   0.375      0.549 0.884 0.096 0.020
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.4462      0.631 0.256 0.004 0.736 0.004
#&gt; SRR1946691     2  0.4428      0.586 0.004 0.720 0.000 0.276
#&gt; SRR1946690     2  0.4946      0.601 0.008 0.776 0.052 0.164
#&gt; SRR1946689     4  0.4936      1.000 0.000 0.012 0.316 0.672
#&gt; SRR1946686     1  0.5523      0.463 0.704 0.012 0.248 0.036
#&gt; SRR1946685     2  0.5576      0.217 0.444 0.536 0.020 0.000
#&gt; SRR1946688     2  0.4509      0.577 0.004 0.708 0.000 0.288
#&gt; SRR1946684     1  0.2197      0.709 0.916 0.080 0.000 0.004
#&gt; SRR1946683     1  0.4883      0.407 0.696 0.288 0.000 0.016
#&gt; SRR1946682     2  0.6341      0.639 0.136 0.652 0.000 0.212
#&gt; SRR1946680     3  0.3853      0.141 0.000 0.020 0.820 0.160
#&gt; SRR1946681     2  0.6922      0.400 0.052 0.600 0.304 0.044
#&gt; SRR1946687     3  0.5532      0.624 0.232 0.004 0.708 0.056
#&gt; SRR1946679     2  0.5218      0.640 0.200 0.736 0.064 0.000
#&gt; SRR1946678     1  0.1796      0.711 0.948 0.032 0.004 0.016
#&gt; SRR1946676     2  0.5328      0.629 0.212 0.724 0.064 0.000
#&gt; SRR1946677     2  0.6756      0.634 0.188 0.612 0.000 0.200
#&gt; SRR1946672     3  0.0707      0.409 0.000 0.000 0.980 0.020
#&gt; SRR1946673     1  0.2530      0.697 0.896 0.100 0.000 0.004
#&gt; SRR1946671     1  0.4630      0.482 0.732 0.252 0.000 0.016
#&gt; SRR1946669     1  0.2197      0.709 0.916 0.080 0.000 0.004
#&gt; SRR1946668     1  0.2197      0.709 0.916 0.080 0.000 0.004
#&gt; SRR1946666     3  0.4822      0.632 0.240 0.004 0.736 0.020
#&gt; SRR1946667     4  0.4936      1.000 0.000 0.012 0.316 0.672
#&gt; SRR1946670     2  0.4756      0.694 0.144 0.784 0.000 0.072
#&gt; SRR1946663     2  0.6341      0.639 0.136 0.652 0.000 0.212
#&gt; SRR1946664     2  0.4225      0.608 0.008 0.832 0.052 0.108
#&gt; SRR1946662     1  0.2773      0.687 0.880 0.116 0.000 0.004
#&gt; SRR1946661     2  0.6805      0.627 0.220 0.604 0.000 0.176
#&gt; SRR1946660     2  0.4483      0.581 0.004 0.712 0.000 0.284
#&gt; SRR1946659     3  0.6310      0.566 0.236 0.004 0.656 0.104
#&gt; SRR1946658     2  0.4330      0.699 0.112 0.828 0.012 0.048
#&gt; SRR1946657     2  0.5298      0.600 0.244 0.708 0.048 0.000
#&gt; SRR1946655     3  0.3052      0.264 0.000 0.004 0.860 0.136
#&gt; SRR1946654     3  0.4240      0.622 0.200 0.012 0.784 0.004
#&gt; SRR1946653     3  0.5532      0.624 0.232 0.004 0.708 0.056
#&gt; SRR1946652     2  0.4746      0.558 0.304 0.688 0.008 0.000
#&gt; SRR1946651     2  0.5180      0.642 0.196 0.740 0.064 0.000
#&gt; SRR1946650     2  0.5072      0.662 0.052 0.740 0.000 0.208
#&gt; SRR1946649     1  0.5937     -0.230 0.492 0.472 0.000 0.036
#&gt; SRR1946648     3  0.6581      0.478 0.352 0.040 0.580 0.028
#&gt; SRR1946647     1  0.2197      0.709 0.916 0.080 0.000 0.004
#&gt; SRR1946646     3  0.6892      0.568 0.224 0.092 0.648 0.036
#&gt; SRR1946645     1  0.5696      0.359 0.664 0.292 0.008 0.036
#&gt; SRR1946644     2  0.5253      0.420 0.360 0.624 0.016 0.000
#&gt; SRR1946643     3  0.3052      0.264 0.000 0.004 0.860 0.136
#&gt; SRR1946642     1  0.1771      0.695 0.948 0.012 0.004 0.036
#&gt; SRR1946641     1  0.5596      0.525 0.728 0.004 0.180 0.088
#&gt; SRR1946656     3  0.3052      0.264 0.000 0.004 0.860 0.136
#&gt; SRR1946640     1  0.5596      0.525 0.728 0.004 0.180 0.088
#&gt; SRR1946639     1  0.5596      0.525 0.728 0.004 0.180 0.088
#&gt; SRR1946638     1  0.5596      0.525 0.728 0.004 0.180 0.088
#&gt; SRR1946637     1  0.5596      0.525 0.728 0.004 0.180 0.088
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3   0.441     0.3515 0.000 0.028 0.780 0.152 0.040
#&gt; SRR1946691     1   0.469     0.4605 0.708 0.240 0.000 0.048 0.004
#&gt; SRR1946690     2   0.578    -0.0509 0.428 0.504 0.004 0.056 0.008
#&gt; SRR1946689     4   0.811     0.3780 0.168 0.008 0.156 0.468 0.200
#&gt; SRR1946686     3   0.564     0.3609 0.008 0.040 0.572 0.012 0.368
#&gt; SRR1946685     2   0.397     0.5790 0.012 0.824 0.080 0.004 0.080
#&gt; SRR1946688     1   0.413     0.5099 0.756 0.204 0.000 0.040 0.000
#&gt; SRR1946684     5   0.500     0.8270 0.000 0.196 0.104 0.000 0.700
#&gt; SRR1946683     5   0.764     0.6325 0.080 0.320 0.120 0.012 0.468
#&gt; SRR1946682     1   0.624     0.6184 0.592 0.188 0.000 0.012 0.208
#&gt; SRR1946680     4   0.452     0.7168 0.000 0.020 0.336 0.644 0.000
#&gt; SRR1946681     2   0.508     0.0626 0.008 0.504 0.020 0.468 0.000
#&gt; SRR1946687     3   0.345     0.3701 0.000 0.016 0.848 0.100 0.036
#&gt; SRR1946679     2   0.122     0.6418 0.004 0.964 0.004 0.008 0.020
#&gt; SRR1946678     5   0.520     0.7452 0.008 0.140 0.144 0.000 0.708
#&gt; SRR1946676     2   0.135     0.6416 0.008 0.960 0.004 0.008 0.020
#&gt; SRR1946677     1   0.689     0.5570 0.512 0.248 0.000 0.024 0.216
#&gt; SRR1946672     4   0.460     0.6078 0.000 0.012 0.428 0.560 0.000
#&gt; SRR1946673     5   0.512     0.8246 0.000 0.212 0.104 0.000 0.684
#&gt; SRR1946671     5   0.763     0.6574 0.080 0.304 0.124 0.012 0.480
#&gt; SRR1946669     5   0.498     0.8242 0.000 0.188 0.108 0.000 0.704
#&gt; SRR1946668     5   0.501     0.8272 0.000 0.192 0.108 0.000 0.700
#&gt; SRR1946666     3   0.421     0.3499 0.000 0.024 0.788 0.156 0.032
#&gt; SRR1946667     4   0.811     0.3780 0.168 0.008 0.156 0.468 0.200
#&gt; SRR1946670     2   0.373     0.4840 0.160 0.804 0.000 0.004 0.032
#&gt; SRR1946663     1   0.621     0.6199 0.596 0.188 0.000 0.012 0.204
#&gt; SRR1946664     2   0.566     0.1036 0.364 0.568 0.004 0.056 0.008
#&gt; SRR1946662     5   0.474     0.7775 0.000 0.272 0.048 0.000 0.680
#&gt; SRR1946661     1   0.702     0.4007 0.420 0.308 0.000 0.012 0.260
#&gt; SRR1946660     1   0.428     0.5081 0.752 0.204 0.000 0.040 0.004
#&gt; SRR1946659     3   0.200     0.4170 0.032 0.000 0.928 0.004 0.036
#&gt; SRR1946658     2   0.315     0.5128 0.136 0.840 0.000 0.000 0.024
#&gt; SRR1946657     2   0.181     0.6418 0.004 0.940 0.012 0.008 0.036
#&gt; SRR1946655     4   0.436     0.7201 0.000 0.012 0.340 0.648 0.000
#&gt; SRR1946654     3   0.522     0.1316 0.000 0.036 0.680 0.252 0.032
#&gt; SRR1946653     3   0.343     0.3664 0.000 0.016 0.848 0.104 0.032
#&gt; SRR1946652     2   0.280     0.6048 0.008 0.876 0.008 0.004 0.104
#&gt; SRR1946651     2   0.122     0.6418 0.004 0.964 0.004 0.008 0.020
#&gt; SRR1946650     1   0.589     0.5435 0.572 0.340 0.000 0.020 0.068
#&gt; SRR1946649     2   0.797    -0.4650 0.096 0.408 0.124 0.016 0.356
#&gt; SRR1946648     3   0.606     0.4171 0.008 0.076 0.680 0.064 0.172
#&gt; SRR1946647     5   0.501     0.8272 0.000 0.192 0.108 0.000 0.700
#&gt; SRR1946646     3   0.582     0.0437 0.000 0.424 0.508 0.040 0.028
#&gt; SRR1946645     5   0.801     0.6062 0.088 0.316 0.148 0.016 0.432
#&gt; SRR1946644     2   0.413     0.5872 0.012 0.816 0.096 0.008 0.068
#&gt; SRR1946643     4   0.436     0.7201 0.000 0.012 0.340 0.648 0.000
#&gt; SRR1946642     5   0.536     0.6186 0.016 0.092 0.200 0.000 0.692
#&gt; SRR1946641     3   0.524     0.3691 0.048 0.000 0.544 0.000 0.408
#&gt; SRR1946656     4   0.436     0.7201 0.000 0.012 0.340 0.648 0.000
#&gt; SRR1946640     3   0.524     0.3691 0.048 0.000 0.544 0.000 0.408
#&gt; SRR1946639     3   0.524     0.3594 0.048 0.000 0.540 0.000 0.412
#&gt; SRR1946638     3   0.524     0.3691 0.048 0.000 0.544 0.000 0.408
#&gt; SRR1946637     3   0.524     0.3691 0.048 0.000 0.544 0.000 0.408
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.3698     0.6716 0.048 0.020 0.804 0.000 0.128 0.000
#&gt; SRR1946691     4  0.5139    -0.1910 0.000 0.084 0.000 0.492 0.000 0.424
#&gt; SRR1946690     4  0.5601     0.2581 0.000 0.324 0.004 0.528 0.000 0.144
#&gt; SRR1946689     4  0.7731     0.2223 0.192 0.000 0.188 0.440 0.032 0.148
#&gt; SRR1946686     3  0.5630     0.4653 0.060 0.040 0.564 0.004 0.332 0.000
#&gt; SRR1946685     2  0.3316     0.7514 0.004 0.844 0.040 0.012 0.096 0.004
#&gt; SRR1946688     6  0.4983    -0.0142 0.004 0.056 0.000 0.456 0.000 0.484
#&gt; SRR1946684     5  0.1910     0.5873 0.000 0.108 0.000 0.000 0.892 0.000
#&gt; SRR1946683     5  0.6808     0.3163 0.016 0.248 0.036 0.012 0.524 0.164
#&gt; SRR1946682     6  0.4071     0.6236 0.004 0.092 0.004 0.004 0.116 0.780
#&gt; SRR1946680     1  0.4184     0.7637 0.556 0.008 0.432 0.000 0.004 0.000
#&gt; SRR1946681     1  0.4622    -0.0745 0.492 0.480 0.016 0.008 0.000 0.004
#&gt; SRR1946687     3  0.2678     0.6925 0.000 0.020 0.860 0.000 0.116 0.004
#&gt; SRR1946679     2  0.0291     0.7722 0.000 0.992 0.000 0.000 0.004 0.004
#&gt; SRR1946678     5  0.1923     0.5710 0.004 0.064 0.016 0.000 0.916 0.000
#&gt; SRR1946676     2  0.0436     0.7752 0.000 0.988 0.004 0.000 0.004 0.004
#&gt; SRR1946677     6  0.5303     0.5945 0.012 0.132 0.012 0.012 0.136 0.696
#&gt; SRR1946672     1  0.4091     0.7034 0.520 0.008 0.472 0.000 0.000 0.000
#&gt; SRR1946673     5  0.2454     0.5637 0.000 0.160 0.000 0.000 0.840 0.000
#&gt; SRR1946671     5  0.6658     0.3358 0.016 0.240 0.032 0.012 0.544 0.156
#&gt; SRR1946669     5  0.1863     0.5890 0.000 0.104 0.000 0.000 0.896 0.000
#&gt; SRR1946668     5  0.1863     0.5890 0.000 0.104 0.000 0.000 0.896 0.000
#&gt; SRR1946666     3  0.3417     0.6713 0.044 0.020 0.828 0.000 0.108 0.000
#&gt; SRR1946667     4  0.7731     0.2223 0.192 0.000 0.188 0.440 0.032 0.148
#&gt; SRR1946670     2  0.4514     0.5977 0.004 0.732 0.008 0.020 0.036 0.200
#&gt; SRR1946663     6  0.3753     0.6204 0.004 0.092 0.000 0.004 0.100 0.800
#&gt; SRR1946664     4  0.5351     0.2691 0.000 0.372 0.004 0.524 0.000 0.100
#&gt; SRR1946662     5  0.2883     0.5297 0.000 0.212 0.000 0.000 0.788 0.000
#&gt; SRR1946661     6  0.6558     0.4023 0.008 0.204 0.004 0.028 0.248 0.508
#&gt; SRR1946660     6  0.4983    -0.0142 0.004 0.056 0.000 0.456 0.000 0.484
#&gt; SRR1946659     3  0.5281     0.3634 0.260 0.000 0.636 0.012 0.080 0.012
#&gt; SRR1946658     2  0.4233     0.6091 0.000 0.748 0.008 0.016 0.036 0.192
#&gt; SRR1946657     2  0.1957     0.7727 0.000 0.920 0.008 0.024 0.048 0.000
#&gt; SRR1946655     1  0.4025     0.7802 0.576 0.008 0.416 0.000 0.000 0.000
#&gt; SRR1946654     3  0.5322     0.3781 0.168 0.052 0.676 0.000 0.104 0.000
#&gt; SRR1946653     3  0.2678     0.6925 0.000 0.020 0.860 0.000 0.116 0.004
#&gt; SRR1946652     2  0.2396     0.7696 0.004 0.892 0.012 0.004 0.084 0.004
#&gt; SRR1946651     2  0.0291     0.7725 0.000 0.992 0.000 0.004 0.004 0.000
#&gt; SRR1946650     6  0.3550     0.5657 0.000 0.188 0.000 0.008 0.024 0.780
#&gt; SRR1946649     5  0.7216     0.2215 0.016 0.304 0.032 0.028 0.456 0.164
#&gt; SRR1946648     3  0.5299     0.5780 0.016 0.040 0.668 0.012 0.240 0.024
#&gt; SRR1946647     5  0.1863     0.5890 0.000 0.104 0.000 0.000 0.896 0.000
#&gt; SRR1946646     2  0.5577     0.1999 0.004 0.508 0.400 0.008 0.072 0.008
#&gt; SRR1946645     5  0.7435     0.2537 0.016 0.232 0.084 0.012 0.472 0.184
#&gt; SRR1946644     2  0.4786     0.6859 0.004 0.740 0.112 0.028 0.112 0.004
#&gt; SRR1946643     1  0.4025     0.7802 0.576 0.008 0.416 0.000 0.000 0.000
#&gt; SRR1946642     5  0.2554     0.5345 0.032 0.032 0.024 0.000 0.900 0.012
#&gt; SRR1946641     5  0.6809     0.1885 0.272 0.000 0.284 0.012 0.408 0.024
#&gt; SRR1946656     1  0.4025     0.7802 0.576 0.008 0.416 0.000 0.000 0.000
#&gt; SRR1946640     5  0.6809     0.1885 0.272 0.000 0.284 0.012 0.408 0.024
#&gt; SRR1946639     5  0.6809     0.1885 0.272 0.000 0.284 0.012 0.408 0.024
#&gt; SRR1946638     5  0.6809     0.1885 0.272 0.000 0.284 0.012 0.408 0.024
#&gt; SRR1946637     5  0.6809     0.1885 0.272 0.000 0.284 0.012 0.408 0.024
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.463           0.794       0.867         0.4967 0.505   0.505
#> 3 3 0.811           0.876       0.931         0.3579 0.688   0.454
#> 4 4 0.642           0.610       0.799         0.1204 0.872   0.630
#> 5 5 0.660           0.649       0.787         0.0664 0.893   0.606
#> 6 6 0.711           0.556       0.753         0.0425 0.921   0.635
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2   0.653     0.8268 0.168 0.832
#&gt; SRR1946691     1   0.821     0.7715 0.744 0.256
#&gt; SRR1946690     1   0.827     0.7677 0.740 0.260
#&gt; SRR1946689     2   0.295     0.7862 0.052 0.948
#&gt; SRR1946686     2   0.821     0.7857 0.256 0.744
#&gt; SRR1946685     1   0.753     0.8250 0.784 0.216
#&gt; SRR1946688     1   0.827     0.7677 0.740 0.260
#&gt; SRR1946684     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946683     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946682     1   0.000     0.8369 1.000 0.000
#&gt; SRR1946680     2   0.295     0.7862 0.052 0.948
#&gt; SRR1946681     1   0.881     0.7276 0.700 0.300
#&gt; SRR1946687     2   0.653     0.8268 0.168 0.832
#&gt; SRR1946679     1   0.671     0.8184 0.824 0.176
#&gt; SRR1946678     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946676     1   0.767     0.7958 0.776 0.224
#&gt; SRR1946677     1   0.000     0.8369 1.000 0.000
#&gt; SRR1946672     2   0.000     0.8058 0.000 1.000
#&gt; SRR1946673     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946671     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946669     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946668     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946666     2   0.653     0.8268 0.168 0.832
#&gt; SRR1946667     2   0.295     0.7862 0.052 0.948
#&gt; SRR1946670     1   0.689     0.8156 0.816 0.184
#&gt; SRR1946663     1   0.000     0.8369 1.000 0.000
#&gt; SRR1946664     1   0.821     0.7715 0.744 0.256
#&gt; SRR1946662     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946661     1   0.000     0.8369 1.000 0.000
#&gt; SRR1946660     1   0.821     0.7715 0.744 0.256
#&gt; SRR1946659     2   0.653     0.8268 0.168 0.832
#&gt; SRR1946658     1   0.767     0.7954 0.776 0.224
#&gt; SRR1946657     1   0.662     0.8218 0.828 0.172
#&gt; SRR1946655     2   0.295     0.7862 0.052 0.948
#&gt; SRR1946654     2   0.000     0.8058 0.000 1.000
#&gt; SRR1946653     2   0.605     0.8282 0.148 0.852
#&gt; SRR1946652     1   0.653     0.8204 0.832 0.168
#&gt; SRR1946651     1   0.662     0.8195 0.828 0.172
#&gt; SRR1946650     1   0.595     0.8279 0.856 0.144
#&gt; SRR1946649     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946648     2   0.662     0.8253 0.172 0.828
#&gt; SRR1946647     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946646     2   0.000     0.8058 0.000 1.000
#&gt; SRR1946645     1   0.430     0.7961 0.912 0.088
#&gt; SRR1946644     2   0.939     0.0936 0.356 0.644
#&gt; SRR1946643     2   0.295     0.7862 0.052 0.948
#&gt; SRR1946642     1   0.295     0.8289 0.948 0.052
#&gt; SRR1946641     2   0.827     0.7835 0.260 0.740
#&gt; SRR1946656     2   0.295     0.7862 0.052 0.948
#&gt; SRR1946640     2   0.827     0.7835 0.260 0.740
#&gt; SRR1946639     2   0.827     0.7835 0.260 0.740
#&gt; SRR1946638     2   0.827     0.7835 0.260 0.740
#&gt; SRR1946637     2   0.827     0.7835 0.260 0.740
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.2625      0.911 0.084 0.000 0.916
#&gt; SRR1946691     2  0.0000      0.911 0.000 1.000 0.000
#&gt; SRR1946690     2  0.2356      0.904 0.000 0.928 0.072
#&gt; SRR1946689     3  0.3192      0.888 0.000 0.112 0.888
#&gt; SRR1946686     1  0.5882      0.431 0.652 0.000 0.348
#&gt; SRR1946685     1  0.8157      0.343 0.596 0.308 0.096
#&gt; SRR1946688     2  0.0000      0.911 0.000 1.000 0.000
#&gt; SRR1946684     1  0.0000      0.943 1.000 0.000 0.000
#&gt; SRR1946683     1  0.0592      0.937 0.988 0.012 0.000
#&gt; SRR1946682     2  0.0892      0.909 0.020 0.980 0.000
#&gt; SRR1946680     3  0.0747      0.922 0.000 0.016 0.984
#&gt; SRR1946681     2  0.4399      0.823 0.000 0.812 0.188
#&gt; SRR1946687     3  0.2711      0.909 0.088 0.000 0.912
#&gt; SRR1946679     2  0.2945      0.898 0.004 0.908 0.088
#&gt; SRR1946678     1  0.0000      0.943 1.000 0.000 0.000
#&gt; SRR1946676     2  0.3349      0.889 0.004 0.888 0.108
#&gt; SRR1946677     2  0.1765      0.898 0.040 0.956 0.004
#&gt; SRR1946672     3  0.0000      0.927 0.000 0.000 1.000
#&gt; SRR1946673     1  0.0000      0.943 1.000 0.000 0.000
#&gt; SRR1946671     1  0.0000      0.943 1.000 0.000 0.000
#&gt; SRR1946669     1  0.0000      0.943 1.000 0.000 0.000
#&gt; SRR1946668     1  0.0000      0.943 1.000 0.000 0.000
#&gt; SRR1946666     3  0.2625      0.911 0.084 0.000 0.916
#&gt; SRR1946667     3  0.3192      0.888 0.000 0.112 0.888
#&gt; SRR1946670     2  0.0237      0.911 0.004 0.996 0.000
#&gt; SRR1946663     2  0.0892      0.909 0.020 0.980 0.000
#&gt; SRR1946664     2  0.2356      0.904 0.000 0.928 0.072
#&gt; SRR1946662     1  0.0237      0.942 0.996 0.004 0.000
#&gt; SRR1946661     2  0.0747      0.910 0.016 0.984 0.000
#&gt; SRR1946660     2  0.0000      0.911 0.000 1.000 0.000
#&gt; SRR1946659     3  0.3192      0.891 0.112 0.000 0.888
#&gt; SRR1946658     2  0.0000      0.911 0.000 1.000 0.000
#&gt; SRR1946657     2  0.4007      0.887 0.036 0.880 0.084
#&gt; SRR1946655     3  0.0424      0.926 0.000 0.008 0.992
#&gt; SRR1946654     3  0.0000      0.927 0.000 0.000 1.000
#&gt; SRR1946653     3  0.2625      0.911 0.084 0.000 0.916
#&gt; SRR1946652     2  0.3445      0.899 0.016 0.896 0.088
#&gt; SRR1946651     2  0.2945      0.898 0.004 0.908 0.088
#&gt; SRR1946650     2  0.0592      0.910 0.012 0.988 0.000
#&gt; SRR1946649     2  0.6008      0.454 0.372 0.628 0.000
#&gt; SRR1946648     3  0.4842      0.761 0.224 0.000 0.776
#&gt; SRR1946647     1  0.0000      0.943 1.000 0.000 0.000
#&gt; SRR1946646     3  0.0592      0.924 0.000 0.012 0.988
#&gt; SRR1946645     1  0.1267      0.928 0.972 0.024 0.004
#&gt; SRR1946644     2  0.8295      0.411 0.088 0.548 0.364
#&gt; SRR1946643     3  0.0424      0.926 0.000 0.008 0.992
#&gt; SRR1946642     1  0.0000      0.943 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0892      0.937 0.980 0.000 0.020
#&gt; SRR1946656     3  0.0424      0.926 0.000 0.008 0.992
#&gt; SRR1946640     1  0.0892      0.937 0.980 0.000 0.020
#&gt; SRR1946639     1  0.0892      0.937 0.980 0.000 0.020
#&gt; SRR1946638     1  0.0892      0.937 0.980 0.000 0.020
#&gt; SRR1946637     1  0.0892      0.937 0.980 0.000 0.020
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.0779     0.8872 0.016 0.004 0.980 0.000
#&gt; SRR1946691     4  0.4916     0.0934 0.000 0.424 0.000 0.576
#&gt; SRR1946690     2  0.3873     0.6677 0.000 0.772 0.000 0.228
#&gt; SRR1946689     3  0.3266     0.8019 0.000 0.000 0.832 0.168
#&gt; SRR1946686     1  0.4661     0.3552 0.652 0.000 0.348 0.000
#&gt; SRR1946685     2  0.3039     0.7511 0.052 0.900 0.012 0.036
#&gt; SRR1946688     4  0.4776     0.2104 0.000 0.376 0.000 0.624
#&gt; SRR1946684     1  0.5496     0.6499 0.652 0.036 0.000 0.312
#&gt; SRR1946683     4  0.6734    -0.2493 0.380 0.084 0.004 0.532
#&gt; SRR1946682     4  0.0592     0.5516 0.000 0.016 0.000 0.984
#&gt; SRR1946680     3  0.2125     0.8932 0.000 0.076 0.920 0.004
#&gt; SRR1946681     2  0.4388     0.6974 0.000 0.808 0.132 0.060
#&gt; SRR1946687     3  0.0469     0.8835 0.012 0.000 0.988 0.000
#&gt; SRR1946679     2  0.0524     0.8057 0.000 0.988 0.004 0.008
#&gt; SRR1946678     1  0.3016     0.6959 0.872 0.004 0.004 0.120
#&gt; SRR1946676     2  0.0524     0.8053 0.000 0.988 0.004 0.008
#&gt; SRR1946677     4  0.1716     0.5490 0.000 0.064 0.000 0.936
#&gt; SRR1946672     3  0.1867     0.8945 0.000 0.072 0.928 0.000
#&gt; SRR1946673     1  0.5966     0.6279 0.624 0.060 0.000 0.316
#&gt; SRR1946671     1  0.6799     0.3593 0.464 0.096 0.000 0.440
#&gt; SRR1946669     1  0.5411     0.6514 0.656 0.032 0.000 0.312
#&gt; SRR1946668     1  0.5322     0.6518 0.660 0.028 0.000 0.312
#&gt; SRR1946666     3  0.1022     0.8745 0.032 0.000 0.968 0.000
#&gt; SRR1946667     3  0.3219     0.8059 0.000 0.000 0.836 0.164
#&gt; SRR1946670     4  0.4981    -0.0186 0.000 0.464 0.000 0.536
#&gt; SRR1946663     4  0.0592     0.5500 0.000 0.016 0.000 0.984
#&gt; SRR1946664     2  0.3123     0.7379 0.000 0.844 0.000 0.156
#&gt; SRR1946662     1  0.6835     0.5682 0.560 0.124 0.000 0.316
#&gt; SRR1946661     4  0.1867     0.5460 0.000 0.072 0.000 0.928
#&gt; SRR1946660     4  0.4776     0.2104 0.000 0.376 0.000 0.624
#&gt; SRR1946659     3  0.3975     0.6828 0.240 0.000 0.760 0.000
#&gt; SRR1946658     2  0.5155     0.0628 0.000 0.528 0.004 0.468
#&gt; SRR1946657     2  0.0524     0.8042 0.004 0.988 0.000 0.008
#&gt; SRR1946655     3  0.1940     0.8941 0.000 0.076 0.924 0.000
#&gt; SRR1946654     3  0.1940     0.8941 0.000 0.076 0.924 0.000
#&gt; SRR1946653     3  0.0336     0.8843 0.008 0.000 0.992 0.000
#&gt; SRR1946652     2  0.3542     0.6844 0.060 0.864 0.000 0.076
#&gt; SRR1946651     2  0.0336     0.8053 0.000 0.992 0.000 0.008
#&gt; SRR1946650     4  0.4730     0.2957 0.000 0.364 0.000 0.636
#&gt; SRR1946649     4  0.7216     0.1753 0.180 0.284 0.000 0.536
#&gt; SRR1946648     3  0.5306     0.6717 0.236 0.008 0.720 0.036
#&gt; SRR1946647     1  0.5411     0.6514 0.656 0.032 0.000 0.312
#&gt; SRR1946646     3  0.4126     0.7785 0.004 0.216 0.776 0.004
#&gt; SRR1946645     4  0.7598    -0.1228 0.384 0.084 0.040 0.492
#&gt; SRR1946644     2  0.4939     0.7306 0.032 0.808 0.092 0.068
#&gt; SRR1946643     3  0.1940     0.8941 0.000 0.076 0.924 0.000
#&gt; SRR1946642     1  0.2256     0.6978 0.924 0.000 0.020 0.056
#&gt; SRR1946641     1  0.1867     0.6869 0.928 0.000 0.072 0.000
#&gt; SRR1946656     3  0.1940     0.8941 0.000 0.076 0.924 0.000
#&gt; SRR1946640     1  0.1867     0.6869 0.928 0.000 0.072 0.000
#&gt; SRR1946639     1  0.1867     0.6869 0.928 0.000 0.072 0.000
#&gt; SRR1946638     1  0.1867     0.6869 0.928 0.000 0.072 0.000
#&gt; SRR1946637     1  0.1867     0.6869 0.928 0.000 0.072 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.1444      0.784 0.040 0.000 0.948 0.000 0.012
#&gt; SRR1946691     4  0.2445      0.672 0.004 0.108 0.004 0.884 0.000
#&gt; SRR1946690     2  0.4576      0.291 0.004 0.536 0.004 0.456 0.000
#&gt; SRR1946689     3  0.6225      0.582 0.092 0.028 0.572 0.308 0.000
#&gt; SRR1946686     1  0.5490      0.479 0.592 0.000 0.324 0.000 0.084
#&gt; SRR1946685     2  0.2285      0.768 0.024 0.916 0.004 0.004 0.052
#&gt; SRR1946688     4  0.1787      0.695 0.016 0.044 0.004 0.936 0.000
#&gt; SRR1946684     5  0.0693      0.748 0.012 0.008 0.000 0.000 0.980
#&gt; SRR1946683     5  0.5532      0.600 0.144 0.036 0.004 0.100 0.716
#&gt; SRR1946682     4  0.4727      0.709 0.096 0.012 0.000 0.756 0.136
#&gt; SRR1946680     3  0.3023      0.771 0.028 0.012 0.872 0.088 0.000
#&gt; SRR1946681     2  0.5124      0.492 0.004 0.628 0.320 0.048 0.000
#&gt; SRR1946687     3  0.5078      0.706 0.232 0.024 0.704 0.036 0.004
#&gt; SRR1946679     2  0.1179      0.790 0.000 0.964 0.004 0.016 0.016
#&gt; SRR1946678     5  0.2605      0.608 0.148 0.000 0.000 0.000 0.852
#&gt; SRR1946676     2  0.1087      0.788 0.000 0.968 0.016 0.008 0.008
#&gt; SRR1946677     4  0.6160      0.585 0.124 0.024 0.004 0.632 0.216
#&gt; SRR1946672     3  0.0671      0.790 0.004 0.016 0.980 0.000 0.000
#&gt; SRR1946673     5  0.0992      0.747 0.008 0.024 0.000 0.000 0.968
#&gt; SRR1946671     5  0.4648      0.671 0.140 0.028 0.004 0.052 0.776
#&gt; SRR1946669     5  0.0693      0.748 0.012 0.008 0.000 0.000 0.980
#&gt; SRR1946668     5  0.0566      0.747 0.012 0.004 0.000 0.000 0.984
#&gt; SRR1946666     3  0.2787      0.737 0.136 0.000 0.856 0.004 0.004
#&gt; SRR1946667     3  0.6225      0.582 0.092 0.028 0.572 0.308 0.000
#&gt; SRR1946670     4  0.5013      0.584 0.004 0.228 0.004 0.700 0.064
#&gt; SRR1946663     4  0.3817      0.732 0.084 0.008 0.000 0.824 0.084
#&gt; SRR1946664     2  0.3662      0.621 0.000 0.744 0.004 0.252 0.000
#&gt; SRR1946662     5  0.1365      0.743 0.004 0.040 0.000 0.004 0.952
#&gt; SRR1946661     4  0.5979      0.596 0.104 0.028 0.000 0.636 0.232
#&gt; SRR1946660     4  0.1638      0.705 0.000 0.064 0.004 0.932 0.000
#&gt; SRR1946659     1  0.4557      0.443 0.720 0.004 0.240 0.004 0.032
#&gt; SRR1946658     4  0.5615      0.275 0.008 0.404 0.024 0.544 0.020
#&gt; SRR1946657     2  0.1117      0.790 0.000 0.964 0.000 0.016 0.020
#&gt; SRR1946655     3  0.0609      0.790 0.000 0.020 0.980 0.000 0.000
#&gt; SRR1946654     3  0.1372      0.790 0.024 0.016 0.956 0.004 0.000
#&gt; SRR1946653     3  0.5078      0.706 0.232 0.024 0.704 0.036 0.004
#&gt; SRR1946652     2  0.3067      0.726 0.012 0.856 0.000 0.012 0.120
#&gt; SRR1946651     2  0.0912      0.789 0.000 0.972 0.000 0.016 0.012
#&gt; SRR1946650     4  0.5393      0.686 0.092 0.164 0.000 0.712 0.032
#&gt; SRR1946649     5  0.7642      0.379 0.132 0.180 0.004 0.160 0.524
#&gt; SRR1946648     3  0.7375      0.562 0.168 0.024 0.560 0.052 0.196
#&gt; SRR1946647     5  0.0451      0.748 0.008 0.004 0.000 0.000 0.988
#&gt; SRR1946646     3  0.7915      0.328 0.100 0.316 0.420 0.160 0.004
#&gt; SRR1946645     5  0.8131      0.259 0.332 0.040 0.036 0.208 0.384
#&gt; SRR1946644     2  0.6358      0.557 0.064 0.644 0.040 0.224 0.028
#&gt; SRR1946643     3  0.0609      0.790 0.000 0.020 0.980 0.000 0.000
#&gt; SRR1946642     5  0.4273     -0.186 0.448 0.000 0.000 0.000 0.552
#&gt; SRR1946641     1  0.3452      0.824 0.756 0.000 0.000 0.000 0.244
#&gt; SRR1946656     3  0.0609      0.790 0.000 0.020 0.980 0.000 0.000
#&gt; SRR1946640     1  0.3452      0.824 0.756 0.000 0.000 0.000 0.244
#&gt; SRR1946639     1  0.3452      0.824 0.756 0.000 0.000 0.000 0.244
#&gt; SRR1946638     1  0.3452      0.824 0.756 0.000 0.000 0.000 0.244
#&gt; SRR1946637     1  0.3452      0.824 0.756 0.000 0.000 0.000 0.244
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.2311     0.7136 0.016 0.000 0.880 0.104 0.000 0.000
#&gt; SRR1946691     6  0.5154     0.5120 0.028 0.080 0.000 0.240 0.000 0.652
#&gt; SRR1946690     2  0.6418     0.1395 0.020 0.428 0.000 0.252 0.000 0.300
#&gt; SRR1946689     4  0.4827     0.4293 0.000 0.000 0.276 0.632 0.000 0.092
#&gt; SRR1946686     1  0.5227     0.3993 0.604 0.000 0.292 0.092 0.012 0.000
#&gt; SRR1946685     2  0.4272     0.6208 0.036 0.800 0.016 0.096 0.044 0.008
#&gt; SRR1946688     6  0.4595     0.5049 0.020 0.040 0.000 0.264 0.000 0.676
#&gt; SRR1946684     5  0.0547     0.8575 0.020 0.000 0.000 0.000 0.980 0.000
#&gt; SRR1946683     5  0.6618     0.3203 0.024 0.036 0.000 0.152 0.524 0.264
#&gt; SRR1946682     6  0.1410     0.6080 0.000 0.008 0.000 0.004 0.044 0.944
#&gt; SRR1946680     3  0.2871     0.5858 0.000 0.004 0.804 0.192 0.000 0.000
#&gt; SRR1946681     2  0.5592     0.1870 0.012 0.488 0.424 0.060 0.000 0.016
#&gt; SRR1946687     3  0.4992     0.0599 0.068 0.000 0.472 0.460 0.000 0.000
#&gt; SRR1946679     2  0.0665     0.7118 0.000 0.980 0.000 0.008 0.008 0.004
#&gt; SRR1946678     5  0.2178     0.7506 0.132 0.000 0.000 0.000 0.868 0.000
#&gt; SRR1946676     2  0.0622     0.7098 0.000 0.980 0.012 0.008 0.000 0.000
#&gt; SRR1946677     6  0.4778     0.5390 0.020 0.040 0.000 0.124 0.064 0.752
#&gt; SRR1946672     3  0.0405     0.7579 0.000 0.004 0.988 0.008 0.000 0.000
#&gt; SRR1946673     5  0.0870     0.8518 0.012 0.012 0.000 0.000 0.972 0.004
#&gt; SRR1946671     5  0.5621     0.5273 0.024 0.024 0.000 0.096 0.652 0.204
#&gt; SRR1946669     5  0.0547     0.8575 0.020 0.000 0.000 0.000 0.980 0.000
#&gt; SRR1946668     5  0.0547     0.8575 0.020 0.000 0.000 0.000 0.980 0.000
#&gt; SRR1946666     3  0.4143     0.6128 0.116 0.000 0.756 0.124 0.000 0.004
#&gt; SRR1946667     4  0.4827     0.4293 0.000 0.000 0.276 0.632 0.000 0.092
#&gt; SRR1946670     6  0.6866     0.3968 0.020 0.224 0.000 0.144 0.080 0.532
#&gt; SRR1946663     6  0.1092     0.6072 0.000 0.000 0.000 0.020 0.020 0.960
#&gt; SRR1946664     2  0.5208     0.5318 0.020 0.664 0.000 0.156 0.000 0.160
#&gt; SRR1946662     5  0.1036     0.8481 0.008 0.024 0.000 0.000 0.964 0.004
#&gt; SRR1946661     6  0.4760     0.5619 0.008 0.044 0.000 0.056 0.156 0.736
#&gt; SRR1946660     6  0.4600     0.5330 0.024 0.056 0.000 0.212 0.000 0.708
#&gt; SRR1946659     1  0.3883     0.5800 0.768 0.000 0.144 0.088 0.000 0.000
#&gt; SRR1946658     6  0.6720     0.1990 0.012 0.360 0.020 0.144 0.016 0.448
#&gt; SRR1946657     2  0.2673     0.6940 0.012 0.888 0.000 0.064 0.016 0.020
#&gt; SRR1946655     3  0.0146     0.7577 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1946654     3  0.1082     0.7520 0.000 0.004 0.956 0.040 0.000 0.000
#&gt; SRR1946653     3  0.4903     0.0610 0.060 0.000 0.476 0.464 0.000 0.000
#&gt; SRR1946652     2  0.3547     0.6338 0.004 0.828 0.000 0.024 0.100 0.044
#&gt; SRR1946651     2  0.0520     0.7133 0.000 0.984 0.000 0.008 0.000 0.008
#&gt; SRR1946650     6  0.3224     0.5769 0.000 0.128 0.000 0.036 0.008 0.828
#&gt; SRR1946649     6  0.7777    -0.0447 0.020 0.160 0.000 0.156 0.328 0.336
#&gt; SRR1946648     4  0.7074     0.1618 0.076 0.000 0.296 0.484 0.108 0.036
#&gt; SRR1946647     5  0.0547     0.8575 0.020 0.000 0.000 0.000 0.980 0.000
#&gt; SRR1946646     4  0.6004     0.4183 0.016 0.288 0.160 0.532 0.000 0.004
#&gt; SRR1946645     6  0.8333     0.2601 0.128 0.060 0.028 0.232 0.124 0.428
#&gt; SRR1946644     4  0.6153    -0.1140 0.028 0.428 0.008 0.460 0.024 0.052
#&gt; SRR1946643     3  0.0405     0.7561 0.000 0.004 0.988 0.008 0.000 0.000
#&gt; SRR1946642     1  0.3817     0.2592 0.568 0.000 0.000 0.000 0.432 0.000
#&gt; SRR1946641     1  0.1387     0.8286 0.932 0.000 0.000 0.000 0.068 0.000
#&gt; SRR1946656     3  0.0405     0.7561 0.000 0.004 0.988 0.008 0.000 0.000
#&gt; SRR1946640     1  0.1387     0.8286 0.932 0.000 0.000 0.000 0.068 0.000
#&gt; SRR1946639     1  0.1387     0.8286 0.932 0.000 0.000 0.000 0.068 0.000
#&gt; SRR1946638     1  0.1387     0.8286 0.932 0.000 0.000 0.000 0.068 0.000
#&gt; SRR1946637     1  0.1387     0.8286 0.932 0.000 0.000 0.000 0.068 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.675           0.826       0.915         0.5033 0.491   0.491
#> 3 3 0.433           0.551       0.818         0.2248 0.749   0.549
#> 4 4 0.629           0.647       0.847         0.0758 0.750   0.472
#> 5 5 0.746           0.812       0.905         0.1314 0.822   0.523
#> 6 6 0.806           0.816       0.913         0.0612 0.927   0.718
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.1414      0.905 0.020 0.980
#&gt; SRR1946691     1  0.9850      0.149 0.572 0.428
#&gt; SRR1946690     2  0.2423      0.904 0.040 0.960
#&gt; SRR1946689     2  0.0672      0.904 0.008 0.992
#&gt; SRR1946686     2  0.7299      0.755 0.204 0.796
#&gt; SRR1946685     2  0.3584      0.901 0.068 0.932
#&gt; SRR1946688     2  0.4815      0.881 0.104 0.896
#&gt; SRR1946684     1  0.0938      0.913 0.988 0.012
#&gt; SRR1946683     1  0.1414      0.907 0.980 0.020
#&gt; SRR1946682     1  0.0376      0.912 0.996 0.004
#&gt; SRR1946680     2  0.2778      0.903 0.048 0.952
#&gt; SRR1946681     2  0.2778      0.903 0.048 0.952
#&gt; SRR1946687     2  0.1414      0.905 0.020 0.980
#&gt; SRR1946679     2  0.5519      0.859 0.128 0.872
#&gt; SRR1946678     1  0.1843      0.910 0.972 0.028
#&gt; SRR1946676     2  0.2778      0.903 0.048 0.952
#&gt; SRR1946677     1  0.0672      0.912 0.992 0.008
#&gt; SRR1946672     2  0.0376      0.899 0.004 0.996
#&gt; SRR1946673     1  0.0000      0.912 1.000 0.000
#&gt; SRR1946671     1  0.0672      0.912 0.992 0.008
#&gt; SRR1946669     1  0.1843      0.910 0.972 0.028
#&gt; SRR1946668     1  0.2043      0.910 0.968 0.032
#&gt; SRR1946666     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946667     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946670     1  0.0672      0.912 0.992 0.008
#&gt; SRR1946663     1  0.0672      0.912 0.992 0.008
#&gt; SRR1946664     2  0.2778      0.903 0.048 0.952
#&gt; SRR1946662     1  0.0376      0.912 0.996 0.004
#&gt; SRR1946661     1  0.0376      0.912 0.996 0.004
#&gt; SRR1946660     2  0.9833      0.354 0.424 0.576
#&gt; SRR1946659     2  0.6973      0.758 0.188 0.812
#&gt; SRR1946658     1  0.9881      0.106 0.564 0.436
#&gt; SRR1946657     2  0.8016      0.736 0.244 0.756
#&gt; SRR1946655     2  0.0672      0.904 0.008 0.992
#&gt; SRR1946654     2  0.2043      0.906 0.032 0.968
#&gt; SRR1946653     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946652     1  0.4562      0.841 0.904 0.096
#&gt; SRR1946651     2  0.6712      0.813 0.176 0.824
#&gt; SRR1946650     1  0.0672      0.912 0.992 0.008
#&gt; SRR1946649     1  0.3114      0.881 0.944 0.056
#&gt; SRR1946648     2  0.9170      0.528 0.332 0.668
#&gt; SRR1946647     1  0.2043      0.910 0.968 0.032
#&gt; SRR1946646     2  0.0376      0.899 0.004 0.996
#&gt; SRR1946645     1  0.9996      0.039 0.512 0.488
#&gt; SRR1946644     2  0.8144      0.727 0.252 0.748
#&gt; SRR1946643     2  0.2236      0.904 0.036 0.964
#&gt; SRR1946642     1  0.2423      0.906 0.960 0.040
#&gt; SRR1946641     1  0.2778      0.903 0.952 0.048
#&gt; SRR1946656     2  0.1414      0.904 0.020 0.980
#&gt; SRR1946640     1  0.2778      0.903 0.952 0.048
#&gt; SRR1946639     1  0.2778      0.903 0.952 0.048
#&gt; SRR1946638     1  0.2778      0.903 0.952 0.048
#&gt; SRR1946637     1  0.2778      0.903 0.952 0.048
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.1860     0.7619 0.000 0.052 0.948
#&gt; SRR1946691     2  0.3941     0.5970 0.000 0.844 0.156
#&gt; SRR1946690     3  0.6235     0.3803 0.000 0.436 0.564
#&gt; SRR1946689     3  0.4702     0.6529 0.212 0.000 0.788
#&gt; SRR1946686     1  0.9544     0.2479 0.440 0.364 0.196
#&gt; SRR1946685     3  0.6267     0.3472 0.000 0.452 0.548
#&gt; SRR1946688     3  0.1765     0.7656 0.004 0.040 0.956
#&gt; SRR1946684     2  0.6045    -0.0956 0.380 0.620 0.000
#&gt; SRR1946683     2  0.5202     0.4550 0.008 0.772 0.220
#&gt; SRR1946682     2  0.0000     0.7081 0.000 1.000 0.000
#&gt; SRR1946680     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946681     3  0.6235     0.3803 0.000 0.436 0.564
#&gt; SRR1946687     3  0.0892     0.7791 0.000 0.020 0.980
#&gt; SRR1946679     3  0.6235     0.3803 0.000 0.436 0.564
#&gt; SRR1946678     2  0.6235    -0.2512 0.436 0.564 0.000
#&gt; SRR1946676     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946677     2  0.0000     0.7081 0.000 1.000 0.000
#&gt; SRR1946672     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946673     2  0.0000     0.7081 0.000 1.000 0.000
#&gt; SRR1946671     2  0.0000     0.7081 0.000 1.000 0.000
#&gt; SRR1946669     2  0.6235    -0.2512 0.436 0.564 0.000
#&gt; SRR1946668     2  0.6235    -0.2512 0.436 0.564 0.000
#&gt; SRR1946666     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946667     3  0.4702     0.6529 0.212 0.000 0.788
#&gt; SRR1946670     2  0.0000     0.7081 0.000 1.000 0.000
#&gt; SRR1946663     2  0.1289     0.6909 0.000 0.968 0.032
#&gt; SRR1946664     3  0.6235     0.3803 0.000 0.436 0.564
#&gt; SRR1946662     2  0.0000     0.7081 0.000 1.000 0.000
#&gt; SRR1946661     2  0.0000     0.7081 0.000 1.000 0.000
#&gt; SRR1946660     2  0.5327     0.4173 0.000 0.728 0.272
#&gt; SRR1946659     1  0.6012     0.6777 0.788 0.088 0.124
#&gt; SRR1946658     2  0.3038     0.6459 0.000 0.896 0.104
#&gt; SRR1946657     2  0.4555     0.5543 0.000 0.800 0.200
#&gt; SRR1946655     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946654     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946653     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946652     2  0.1031     0.6990 0.000 0.976 0.024
#&gt; SRR1946651     3  0.6235     0.3803 0.000 0.436 0.564
#&gt; SRR1946650     2  0.0000     0.7081 0.000 1.000 0.000
#&gt; SRR1946649     2  0.0424     0.7059 0.000 0.992 0.008
#&gt; SRR1946648     3  0.6079     0.2416 0.000 0.388 0.612
#&gt; SRR1946647     2  0.6235    -0.2512 0.436 0.564 0.000
#&gt; SRR1946646     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946645     3  0.4702     0.5928 0.000 0.212 0.788
#&gt; SRR1946644     2  0.6225    -0.0948 0.000 0.568 0.432
#&gt; SRR1946643     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946642     1  0.6307     0.3625 0.512 0.488 0.000
#&gt; SRR1946641     1  0.4702     0.8222 0.788 0.212 0.000
#&gt; SRR1946656     3  0.0000     0.7861 0.000 0.000 1.000
#&gt; SRR1946640     1  0.4702     0.8222 0.788 0.212 0.000
#&gt; SRR1946639     1  0.4702     0.8222 0.788 0.212 0.000
#&gt; SRR1946638     1  0.4702     0.8222 0.788 0.212 0.000
#&gt; SRR1946637     1  0.4702     0.8222 0.788 0.212 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.1474      0.890 0.000 0.052 0.948 0.000
#&gt; SRR1946691     2  0.2466      0.679 0.000 0.900 0.096 0.004
#&gt; SRR1946690     2  0.5167      0.294 0.000 0.508 0.488 0.004
#&gt; SRR1946689     4  0.0188      1.000 0.000 0.000 0.004 0.996
#&gt; SRR1946686     1  0.5997      0.586 0.576 0.376 0.048 0.000
#&gt; SRR1946685     2  0.5158      0.322 0.000 0.524 0.472 0.004
#&gt; SRR1946688     3  0.1452      0.902 0.000 0.036 0.956 0.008
#&gt; SRR1946684     2  0.4898     -0.385 0.416 0.584 0.000 0.000
#&gt; SRR1946683     2  0.4621      0.381 0.008 0.708 0.284 0.000
#&gt; SRR1946682     2  0.0000      0.689 0.000 1.000 0.000 0.000
#&gt; SRR1946680     3  0.0336      0.925 0.000 0.008 0.992 0.000
#&gt; SRR1946681     2  0.5168      0.275 0.000 0.500 0.496 0.004
#&gt; SRR1946687     3  0.0817      0.917 0.000 0.024 0.976 0.000
#&gt; SRR1946679     2  0.5167      0.294 0.000 0.508 0.488 0.004
#&gt; SRR1946678     1  0.4999      0.537 0.508 0.492 0.000 0.000
#&gt; SRR1946676     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1946677     2  0.0000      0.689 0.000 1.000 0.000 0.000
#&gt; SRR1946672     3  0.0336      0.924 0.008 0.000 0.992 0.000
#&gt; SRR1946673     2  0.0000      0.689 0.000 1.000 0.000 0.000
#&gt; SRR1946671     2  0.0000      0.689 0.000 1.000 0.000 0.000
#&gt; SRR1946669     1  0.4999      0.537 0.508 0.492 0.000 0.000
#&gt; SRR1946668     1  0.4999      0.537 0.508 0.492 0.000 0.000
#&gt; SRR1946666     3  0.0336      0.924 0.008 0.000 0.992 0.000
#&gt; SRR1946667     4  0.0188      1.000 0.000 0.000 0.004 0.996
#&gt; SRR1946670     2  0.0000      0.689 0.000 1.000 0.000 0.000
#&gt; SRR1946663     2  0.1211      0.669 0.000 0.960 0.040 0.000
#&gt; SRR1946664     2  0.5167      0.294 0.000 0.508 0.488 0.004
#&gt; SRR1946662     2  0.0000      0.689 0.000 1.000 0.000 0.000
#&gt; SRR1946661     2  0.0188      0.690 0.000 0.996 0.000 0.004
#&gt; SRR1946660     2  0.3870      0.637 0.000 0.788 0.208 0.004
#&gt; SRR1946659     1  0.0000      0.585 1.000 0.000 0.000 0.000
#&gt; SRR1946658     2  0.1576      0.690 0.000 0.948 0.048 0.004
#&gt; SRR1946657     2  0.2714      0.671 0.000 0.884 0.112 0.004
#&gt; SRR1946655     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1946654     3  0.0336      0.925 0.000 0.008 0.992 0.000
#&gt; SRR1946653     3  0.0524      0.924 0.008 0.004 0.988 0.000
#&gt; SRR1946652     2  0.0895      0.693 0.000 0.976 0.020 0.004
#&gt; SRR1946651     2  0.5167      0.294 0.000 0.508 0.488 0.004
#&gt; SRR1946650     2  0.0524      0.690 0.000 0.988 0.008 0.004
#&gt; SRR1946649     2  0.0336      0.691 0.000 0.992 0.008 0.000
#&gt; SRR1946648     3  0.4817      0.271 0.000 0.388 0.612 0.000
#&gt; SRR1946647     1  0.4999      0.537 0.508 0.492 0.000 0.000
#&gt; SRR1946646     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1946645     3  0.3311      0.727 0.000 0.172 0.828 0.000
#&gt; SRR1946644     2  0.4950      0.455 0.000 0.620 0.376 0.004
#&gt; SRR1946643     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1946642     1  0.4866      0.600 0.596 0.404 0.000 0.000
#&gt; SRR1946641     1  0.0000      0.585 1.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1946640     1  0.0000      0.585 1.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.585 1.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.585 1.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.585 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.1608      0.871 0.000 0.000 0.928 0.000 0.072
#&gt; SRR1946691     2  0.0000      0.759 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946690     2  0.2690      0.815 0.000 0.844 0.156 0.000 0.000
#&gt; SRR1946689     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946686     5  0.2171      0.820 0.064 0.000 0.024 0.000 0.912
#&gt; SRR1946685     2  0.4014      0.743 0.000 0.728 0.256 0.000 0.016
#&gt; SRR1946688     3  0.3475      0.752 0.000 0.180 0.804 0.004 0.012
#&gt; SRR1946684     5  0.0000      0.871 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946683     5  0.0451      0.869 0.000 0.008 0.004 0.000 0.988
#&gt; SRR1946682     5  0.2424      0.787 0.000 0.132 0.000 0.000 0.868
#&gt; SRR1946680     3  0.0000      0.912 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946681     2  0.4210      0.547 0.000 0.588 0.412 0.000 0.000
#&gt; SRR1946687     3  0.1121      0.895 0.000 0.000 0.956 0.000 0.044
#&gt; SRR1946679     2  0.2773      0.813 0.000 0.836 0.164 0.000 0.000
#&gt; SRR1946678     5  0.0609      0.865 0.020 0.000 0.000 0.000 0.980
#&gt; SRR1946676     3  0.0703      0.906 0.000 0.024 0.976 0.000 0.000
#&gt; SRR1946677     5  0.3636      0.679 0.000 0.272 0.000 0.000 0.728
#&gt; SRR1946672     3  0.0000      0.912 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946673     5  0.0000      0.871 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946671     5  0.0609      0.866 0.000 0.020 0.000 0.000 0.980
#&gt; SRR1946669     5  0.0000      0.871 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946668     5  0.0000      0.871 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946666     3  0.0609      0.909 0.020 0.000 0.980 0.000 0.000
#&gt; SRR1946667     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946670     5  0.0451      0.869 0.000 0.008 0.004 0.000 0.988
#&gt; SRR1946663     5  0.2424      0.787 0.000 0.132 0.000 0.000 0.868
#&gt; SRR1946664     2  0.2471      0.817 0.000 0.864 0.136 0.000 0.000
#&gt; SRR1946662     5  0.0000      0.871 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946661     2  0.4030      0.471 0.000 0.648 0.000 0.000 0.352
#&gt; SRR1946660     2  0.0880      0.759 0.000 0.968 0.000 0.000 0.032
#&gt; SRR1946659     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946658     2  0.3409      0.757 0.000 0.816 0.024 0.000 0.160
#&gt; SRR1946657     2  0.3309      0.780 0.000 0.836 0.036 0.000 0.128
#&gt; SRR1946655     3  0.0000      0.912 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946654     3  0.0579      0.911 0.000 0.008 0.984 0.000 0.008
#&gt; SRR1946653     3  0.0865      0.907 0.024 0.000 0.972 0.000 0.004
#&gt; SRR1946652     5  0.4659     -0.145 0.000 0.492 0.012 0.000 0.496
#&gt; SRR1946651     2  0.2773      0.813 0.000 0.836 0.164 0.000 0.000
#&gt; SRR1946650     2  0.1478      0.758 0.000 0.936 0.000 0.000 0.064
#&gt; SRR1946649     5  0.4321      0.246 0.000 0.396 0.004 0.000 0.600
#&gt; SRR1946648     3  0.4161      0.379 0.000 0.000 0.608 0.000 0.392
#&gt; SRR1946647     5  0.0000      0.871 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946646     3  0.0794      0.904 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1946645     3  0.3639      0.757 0.044 0.000 0.812 0.000 0.144
#&gt; SRR1946644     2  0.3427      0.819 0.000 0.836 0.108 0.000 0.056
#&gt; SRR1946643     3  0.0000      0.912 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946642     5  0.2377      0.786 0.128 0.000 0.000 0.000 0.872
#&gt; SRR1946641     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0000      0.912 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946640     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5    p6
#&gt; SRR1946675     3  0.2260     0.8250 0.000 0.000 0.860  0 0.140 0.000
#&gt; SRR1946691     2  0.1765     0.7555 0.000 0.904 0.000  0 0.000 0.096
#&gt; SRR1946690     2  0.0000     0.7862 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1946689     4  0.0000     1.0000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946686     5  0.1644     0.8764 0.040 0.000 0.028  0 0.932 0.000
#&gt; SRR1946685     2  0.2988     0.6968 0.000 0.828 0.144  0 0.028 0.000
#&gt; SRR1946688     6  0.0520     0.9118 0.000 0.008 0.000  0 0.008 0.984
#&gt; SRR1946684     5  0.0000     0.9333 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946683     5  0.0146     0.9310 0.000 0.000 0.004  0 0.996 0.000
#&gt; SRR1946682     6  0.1444     0.9437 0.000 0.000 0.000  0 0.072 0.928
#&gt; SRR1946680     3  0.0000     0.8540 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946681     2  0.4076     0.4520 0.000 0.592 0.396  0 0.000 0.012
#&gt; SRR1946687     3  0.2219     0.8274 0.000 0.000 0.864  0 0.136 0.000
#&gt; SRR1946679     2  0.0000     0.7862 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1946678     5  0.0146     0.9319 0.004 0.000 0.000  0 0.996 0.000
#&gt; SRR1946676     3  0.2300     0.8094 0.000 0.144 0.856  0 0.000 0.000
#&gt; SRR1946677     6  0.1444     0.9437 0.000 0.000 0.000  0 0.072 0.928
#&gt; SRR1946672     3  0.0622     0.8536 0.012 0.000 0.980  0 0.000 0.008
#&gt; SRR1946673     5  0.0000     0.9333 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946671     5  0.0146     0.9316 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR1946669     5  0.0000     0.9333 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946668     5  0.0000     0.9333 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946666     3  0.2191     0.8255 0.120 0.000 0.876  0 0.004 0.000
#&gt; SRR1946667     4  0.0000     1.0000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946670     5  0.0622     0.9220 0.000 0.008 0.012  0 0.980 0.000
#&gt; SRR1946663     6  0.1444     0.9437 0.000 0.000 0.000  0 0.072 0.928
#&gt; SRR1946664     2  0.0146     0.7857 0.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1946662     5  0.0000     0.9333 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946661     2  0.3899     0.4505 0.000 0.628 0.000  0 0.364 0.008
#&gt; SRR1946660     6  0.0405     0.9130 0.000 0.004 0.000  0 0.008 0.988
#&gt; SRR1946659     1  0.0000     1.0000 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946658     2  0.1625     0.7646 0.000 0.928 0.012  0 0.060 0.000
#&gt; SRR1946657     2  0.0363     0.7876 0.000 0.988 0.000  0 0.012 0.000
#&gt; SRR1946655     3  0.0000     0.8540 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946654     3  0.2019     0.8488 0.000 0.012 0.900  0 0.088 0.000
#&gt; SRR1946653     3  0.2573     0.8319 0.112 0.000 0.864  0 0.024 0.000
#&gt; SRR1946652     2  0.4185     0.0977 0.000 0.496 0.012  0 0.492 0.000
#&gt; SRR1946651     2  0.0000     0.7862 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1946650     2  0.4780     0.3016 0.000 0.552 0.000  0 0.056 0.392
#&gt; SRR1946649     5  0.3881     0.1671 0.000 0.396 0.004  0 0.600 0.000
#&gt; SRR1946648     3  0.3727     0.4638 0.000 0.000 0.612  0 0.388 0.000
#&gt; SRR1946647     5  0.0000     0.9333 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946646     3  0.2572     0.8101 0.012 0.136 0.852  0 0.000 0.000
#&gt; SRR1946645     3  0.3912     0.7168 0.044 0.000 0.732  0 0.224 0.000
#&gt; SRR1946644     2  0.0363     0.7876 0.000 0.988 0.000  0 0.012 0.000
#&gt; SRR1946643     3  0.0363     0.8512 0.000 0.000 0.988  0 0.000 0.012
#&gt; SRR1946642     5  0.2092     0.7969 0.124 0.000 0.000  0 0.876 0.000
#&gt; SRR1946641     1  0.0000     1.0000 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946656     3  0.0363     0.8512 0.000 0.000 0.988  0 0.000 0.012
#&gt; SRR1946640     1  0.0000     1.0000 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946639     1  0.0000     1.0000 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946638     1  0.0000     1.0000 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946637     1  0.0000     1.0000 1.000 0.000 0.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.484           0.876       0.905         0.3089 0.713   0.713
#> 3 3 0.334           0.661       0.783         0.8694 0.441   0.352
#> 4 4 0.376           0.696       0.754         0.1676 0.706   0.434
#> 5 5 0.590           0.535       0.721         0.0999 0.877   0.649
#> 6 6 0.633           0.691       0.733         0.0499 0.819   0.439
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946691     2  0.7815      0.865 0.232 0.768
#&gt; SRR1946690     1  0.5737      0.847 0.864 0.136
#&gt; SRR1946689     2  0.4161      0.895 0.084 0.916
#&gt; SRR1946686     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946685     1  0.3114      0.888 0.944 0.056
#&gt; SRR1946688     2  0.7674      0.874 0.224 0.776
#&gt; SRR1946684     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946683     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946682     1  0.5737      0.847 0.864 0.136
#&gt; SRR1946680     2  0.8207      0.808 0.256 0.744
#&gt; SRR1946681     1  0.5629      0.849 0.868 0.132
#&gt; SRR1946687     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946679     1  0.6531      0.813 0.832 0.168
#&gt; SRR1946678     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946676     1  0.5946      0.840 0.856 0.144
#&gt; SRR1946677     1  0.6887      0.844 0.816 0.184
#&gt; SRR1946672     1  0.5737      0.848 0.864 0.136
#&gt; SRR1946673     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946671     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946669     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946668     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946666     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946667     2  0.4161      0.895 0.084 0.916
#&gt; SRR1946670     1  0.5737      0.847 0.864 0.136
#&gt; SRR1946663     1  0.5737      0.847 0.864 0.136
#&gt; SRR1946664     1  0.5737      0.847 0.864 0.136
#&gt; SRR1946662     1  0.3879      0.878 0.924 0.076
#&gt; SRR1946661     1  0.5946      0.849 0.856 0.144
#&gt; SRR1946660     2  0.7674      0.874 0.224 0.776
#&gt; SRR1946659     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946658     1  0.5946      0.840 0.856 0.144
#&gt; SRR1946657     1  0.4690      0.868 0.900 0.100
#&gt; SRR1946655     2  0.5178      0.913 0.116 0.884
#&gt; SRR1946654     1  0.4431      0.874 0.908 0.092
#&gt; SRR1946653     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946652     1  0.0938      0.904 0.988 0.012
#&gt; SRR1946651     1  0.6343      0.823 0.840 0.160
#&gt; SRR1946650     1  0.5737      0.847 0.864 0.136
#&gt; SRR1946649     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946648     1  0.2423      0.894 0.960 0.040
#&gt; SRR1946647     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946646     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946645     1  0.4161      0.874 0.916 0.084
#&gt; SRR1946644     1  0.2236      0.894 0.964 0.036
#&gt; SRR1946643     2  0.5178      0.913 0.116 0.884
#&gt; SRR1946642     1  0.0000      0.904 1.000 0.000
#&gt; SRR1946641     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946656     2  0.5178      0.913 0.116 0.884
#&gt; SRR1946640     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946639     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946638     1  0.0376      0.904 0.996 0.004
#&gt; SRR1946637     1  0.0376      0.904 0.996 0.004
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     2  0.5397     0.6342 0.280 0.720 0.000
#&gt; SRR1946691     2  0.0747     0.7037 0.000 0.984 0.016
#&gt; SRR1946690     2  0.0747     0.7073 0.016 0.984 0.000
#&gt; SRR1946689     2  0.5397     0.6680 0.000 0.720 0.280
#&gt; SRR1946686     2  0.5254     0.6417 0.264 0.736 0.000
#&gt; SRR1946685     1  0.1031     0.8144 0.976 0.024 0.000
#&gt; SRR1946688     2  0.1163     0.7048 0.000 0.972 0.028
#&gt; SRR1946684     1  0.0000     0.8250 1.000 0.000 0.000
#&gt; SRR1946683     1  0.0237     0.8240 0.996 0.004 0.000
#&gt; SRR1946682     2  0.6824     0.0741 0.408 0.576 0.016
#&gt; SRR1946680     2  0.6906     0.6838 0.084 0.724 0.192
#&gt; SRR1946681     2  0.2703     0.7124 0.056 0.928 0.016
#&gt; SRR1946687     2  0.7163     0.6797 0.136 0.720 0.144
#&gt; SRR1946679     2  0.5859     0.3595 0.344 0.656 0.000
#&gt; SRR1946678     1  0.0000     0.8250 1.000 0.000 0.000
#&gt; SRR1946676     2  0.3116     0.6889 0.108 0.892 0.000
#&gt; SRR1946677     1  0.6359     0.5118 0.628 0.364 0.008
#&gt; SRR1946672     2  0.6662     0.6858 0.072 0.736 0.192
#&gt; SRR1946673     1  0.0592     0.8236 0.988 0.012 0.000
#&gt; SRR1946671     1  0.0000     0.8250 1.000 0.000 0.000
#&gt; SRR1946669     1  0.0000     0.8250 1.000 0.000 0.000
#&gt; SRR1946668     1  0.0237     0.8250 0.996 0.004 0.000
#&gt; SRR1946666     2  0.5588     0.6358 0.276 0.720 0.004
#&gt; SRR1946667     2  0.5397     0.6680 0.000 0.720 0.280
#&gt; SRR1946670     2  0.6079     0.1859 0.388 0.612 0.000
#&gt; SRR1946663     2  0.2703     0.6851 0.056 0.928 0.016
#&gt; SRR1946664     2  0.0747     0.7073 0.016 0.984 0.000
#&gt; SRR1946662     1  0.3816     0.7252 0.852 0.148 0.000
#&gt; SRR1946661     1  0.6769     0.4553 0.592 0.392 0.016
#&gt; SRR1946660     2  0.0747     0.7037 0.000 0.984 0.016
#&gt; SRR1946659     2  0.6565     0.6506 0.232 0.720 0.048
#&gt; SRR1946658     2  0.6018     0.4048 0.308 0.684 0.008
#&gt; SRR1946657     2  0.6252     0.0548 0.444 0.556 0.000
#&gt; SRR1946655     2  0.5443     0.6701 0.004 0.736 0.260
#&gt; SRR1946654     2  0.5254     0.6417 0.264 0.736 0.000
#&gt; SRR1946653     2  0.7155     0.6808 0.128 0.720 0.152
#&gt; SRR1946652     1  0.6062     0.4383 0.616 0.384 0.000
#&gt; SRR1946651     2  0.5706     0.4109 0.320 0.680 0.000
#&gt; SRR1946650     2  0.6161     0.4029 0.288 0.696 0.016
#&gt; SRR1946649     1  0.3412     0.7517 0.876 0.124 0.000
#&gt; SRR1946648     2  0.5968     0.5208 0.364 0.636 0.000
#&gt; SRR1946647     1  0.0000     0.8250 1.000 0.000 0.000
#&gt; SRR1946646     2  0.4931     0.6574 0.232 0.768 0.000
#&gt; SRR1946645     1  0.0000     0.8250 1.000 0.000 0.000
#&gt; SRR1946644     2  0.6309     0.2122 0.496 0.504 0.000
#&gt; SRR1946643     2  0.5580     0.6716 0.008 0.736 0.256
#&gt; SRR1946642     1  0.2537     0.7514 0.920 0.080 0.000
#&gt; SRR1946641     3  0.5397     0.9982 0.280 0.000 0.720
#&gt; SRR1946656     2  0.5443     0.6701 0.004 0.736 0.260
#&gt; SRR1946640     3  0.5397     0.9982 0.280 0.000 0.720
#&gt; SRR1946639     3  0.5623     0.9930 0.280 0.004 0.716
#&gt; SRR1946638     3  0.5397     0.9982 0.280 0.000 0.720
#&gt; SRR1946637     3  0.5397     0.9982 0.280 0.000 0.720
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.1807     0.7044 0.008 0.052 0.940 0.000
#&gt; SRR1946691     2  0.1356     0.7426 0.008 0.960 0.032 0.000
#&gt; SRR1946690     2  0.4287     0.7388 0.088 0.828 0.080 0.004
#&gt; SRR1946689     3  0.6096     0.5682 0.044 0.004 0.576 0.376
#&gt; SRR1946686     3  0.3286     0.6522 0.044 0.080 0.876 0.000
#&gt; SRR1946685     2  0.6488     0.4122 0.244 0.628 0.128 0.000
#&gt; SRR1946688     2  0.5353    -0.0747 0.012 0.556 0.432 0.000
#&gt; SRR1946684     1  0.5676     0.8921 0.720 0.144 0.136 0.000
#&gt; SRR1946683     1  0.7058     0.5491 0.520 0.344 0.136 0.000
#&gt; SRR1946682     2  0.0336     0.7429 0.008 0.992 0.000 0.000
#&gt; SRR1946680     3  0.7657     0.6923 0.192 0.052 0.604 0.152
#&gt; SRR1946681     3  0.7738     0.4155 0.300 0.224 0.472 0.004
#&gt; SRR1946687     3  0.1389     0.7038 0.000 0.048 0.952 0.000
#&gt; SRR1946679     2  0.5288     0.7087 0.196 0.740 0.060 0.004
#&gt; SRR1946678     1  0.5417     0.7495 0.704 0.056 0.240 0.000
#&gt; SRR1946676     2  0.6176     0.6764 0.200 0.680 0.116 0.004
#&gt; SRR1946677     2  0.3710     0.6445 0.192 0.804 0.004 0.000
#&gt; SRR1946672     3  0.6929     0.7052 0.144 0.052 0.676 0.128
#&gt; SRR1946673     1  0.5849     0.8839 0.704 0.164 0.132 0.000
#&gt; SRR1946671     1  0.5897     0.8859 0.700 0.164 0.136 0.000
#&gt; SRR1946669     1  0.5677     0.8909 0.720 0.140 0.140 0.000
#&gt; SRR1946668     1  0.5722     0.8916 0.716 0.148 0.136 0.000
#&gt; SRR1946666     3  0.1389     0.7038 0.000 0.048 0.952 0.000
#&gt; SRR1946667     3  0.6096     0.5682 0.044 0.004 0.576 0.376
#&gt; SRR1946670     2  0.0779     0.7520 0.004 0.980 0.016 0.000
#&gt; SRR1946663     2  0.0592     0.7470 0.000 0.984 0.016 0.000
#&gt; SRR1946664     2  0.4287     0.7388 0.088 0.828 0.080 0.004
#&gt; SRR1946662     1  0.5395     0.8071 0.732 0.184 0.084 0.000
#&gt; SRR1946661     2  0.1118     0.7237 0.036 0.964 0.000 0.000
#&gt; SRR1946660     2  0.1488     0.7407 0.012 0.956 0.032 0.000
#&gt; SRR1946659     3  0.1661     0.7035 0.004 0.052 0.944 0.000
#&gt; SRR1946658     2  0.3181     0.7569 0.044 0.888 0.064 0.004
#&gt; SRR1946657     2  0.5905     0.6707 0.200 0.700 0.096 0.004
#&gt; SRR1946655     3  0.7332     0.6917 0.152 0.048 0.636 0.164
#&gt; SRR1946654     3  0.2928     0.7151 0.052 0.052 0.896 0.000
#&gt; SRR1946653     3  0.1389     0.7038 0.000 0.048 0.952 0.000
#&gt; SRR1946652     2  0.5842     0.6353 0.220 0.688 0.092 0.000
#&gt; SRR1946651     2  0.4277     0.7432 0.116 0.824 0.056 0.004
#&gt; SRR1946650     2  0.0000     0.7459 0.000 1.000 0.000 0.000
#&gt; SRR1946649     2  0.6708     0.3319 0.272 0.596 0.132 0.000
#&gt; SRR1946648     3  0.3758     0.6544 0.104 0.048 0.848 0.000
#&gt; SRR1946647     1  0.5724     0.8886 0.716 0.140 0.144 0.000
#&gt; SRR1946646     3  0.4568     0.6377 0.076 0.124 0.800 0.000
#&gt; SRR1946645     2  0.7287    -0.2049 0.384 0.464 0.152 0.000
#&gt; SRR1946644     2  0.6352     0.5475 0.156 0.656 0.188 0.000
#&gt; SRR1946643     3  0.7332     0.6917 0.152 0.048 0.636 0.164
#&gt; SRR1946642     1  0.5417     0.7496 0.704 0.056 0.240 0.000
#&gt; SRR1946641     4  0.5713     0.9968 0.040 0.000 0.340 0.620
#&gt; SRR1946656     3  0.7332     0.6917 0.152 0.048 0.636 0.164
#&gt; SRR1946640     4  0.5713     0.9968 0.040 0.000 0.340 0.620
#&gt; SRR1946639     4  0.5746     0.9872 0.040 0.000 0.348 0.612
#&gt; SRR1946638     4  0.5713     0.9968 0.040 0.000 0.340 0.620
#&gt; SRR1946637     4  0.5713     0.9968 0.040 0.000 0.340 0.620
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.1106      0.472 0.000 0.012 0.964 0.000 0.024
#&gt; SRR1946691     2  0.4030      0.730 0.000 0.648 0.000 0.352 0.000
#&gt; SRR1946690     2  0.1661      0.728 0.000 0.940 0.024 0.036 0.000
#&gt; SRR1946689     4  0.5664      1.000 0.220 0.000 0.152 0.628 0.000
#&gt; SRR1946686     3  0.3463      0.458 0.040 0.044 0.860 0.000 0.056
#&gt; SRR1946685     2  0.4242      0.398 0.000 0.572 0.000 0.000 0.428
#&gt; SRR1946688     2  0.4166      0.730 0.000 0.648 0.004 0.348 0.000
#&gt; SRR1946684     5  0.0162      0.844 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1946683     5  0.1571      0.816 0.004 0.060 0.000 0.000 0.936
#&gt; SRR1946682     2  0.4668      0.743 0.000 0.624 0.000 0.352 0.024
#&gt; SRR1946680     3  0.6427      0.167 0.072 0.332 0.552 0.040 0.004
#&gt; SRR1946681     2  0.3820      0.700 0.016 0.836 0.084 0.004 0.060
#&gt; SRR1946687     3  0.0960      0.456 0.008 0.000 0.972 0.016 0.004
#&gt; SRR1946679     2  0.2291      0.728 0.012 0.908 0.000 0.008 0.072
#&gt; SRR1946678     5  0.1661      0.803 0.024 0.000 0.036 0.000 0.940
#&gt; SRR1946676     2  0.2387      0.728 0.012 0.908 0.004 0.008 0.068
#&gt; SRR1946677     2  0.6378      0.579 0.000 0.528 0.004 0.180 0.288
#&gt; SRR1946672     3  0.4237      0.491 0.152 0.076 0.772 0.000 0.000
#&gt; SRR1946673     5  0.0566      0.845 0.004 0.012 0.000 0.000 0.984
#&gt; SRR1946671     5  0.0404      0.845 0.000 0.012 0.000 0.000 0.988
#&gt; SRR1946669     5  0.0324      0.843 0.004 0.000 0.004 0.000 0.992
#&gt; SRR1946668     5  0.0162      0.844 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1946666     3  0.0324      0.444 0.004 0.000 0.992 0.000 0.004
#&gt; SRR1946667     4  0.5664      1.000 0.220 0.000 0.152 0.628 0.000
#&gt; SRR1946670     2  0.5571      0.748 0.000 0.600 0.020 0.332 0.048
#&gt; SRR1946663     2  0.4030      0.730 0.000 0.648 0.000 0.352 0.000
#&gt; SRR1946664     2  0.1605      0.732 0.004 0.944 0.012 0.040 0.000
#&gt; SRR1946662     5  0.1662      0.812 0.004 0.056 0.000 0.004 0.936
#&gt; SRR1946661     2  0.5006      0.744 0.000 0.624 0.000 0.328 0.048
#&gt; SRR1946660     2  0.4030      0.730 0.000 0.648 0.000 0.352 0.000
#&gt; SRR1946659     3  0.1121      0.461 0.008 0.004 0.968 0.016 0.004
#&gt; SRR1946658     2  0.2844      0.745 0.000 0.888 0.032 0.016 0.064
#&gt; SRR1946657     2  0.2989      0.715 0.008 0.852 0.000 0.008 0.132
#&gt; SRR1946655     3  0.6155      0.112 0.428 0.076 0.476 0.020 0.000
#&gt; SRR1946654     3  0.3436      0.499 0.012 0.080 0.852 0.000 0.056
#&gt; SRR1946653     3  0.0960      0.462 0.008 0.000 0.972 0.016 0.004
#&gt; SRR1946652     2  0.3333      0.672 0.000 0.788 0.000 0.004 0.208
#&gt; SRR1946651     2  0.2115      0.731 0.008 0.916 0.000 0.008 0.068
#&gt; SRR1946650     2  0.4846      0.743 0.004 0.612 0.000 0.360 0.024
#&gt; SRR1946649     5  0.4443     -0.204 0.004 0.472 0.000 0.000 0.524
#&gt; SRR1946648     3  0.3972      0.383 0.008 0.000 0.764 0.016 0.212
#&gt; SRR1946647     5  0.0324      0.845 0.004 0.004 0.000 0.000 0.992
#&gt; SRR1946646     3  0.5475      0.435 0.008 0.132 0.712 0.016 0.132
#&gt; SRR1946645     5  0.4118      0.306 0.004 0.336 0.000 0.000 0.660
#&gt; SRR1946644     2  0.5764      0.500 0.004 0.572 0.024 0.040 0.360
#&gt; SRR1946643     3  0.6076      0.116 0.432 0.076 0.476 0.016 0.000
#&gt; SRR1946642     5  0.2848      0.730 0.028 0.000 0.104 0.000 0.868
#&gt; SRR1946641     1  0.4748      1.000 0.492 0.000 0.492 0.000 0.016
#&gt; SRR1946656     3  0.6076      0.116 0.432 0.076 0.476 0.016 0.000
#&gt; SRR1946640     1  0.4748      1.000 0.492 0.000 0.492 0.000 0.016
#&gt; SRR1946639     3  0.4723     -0.899 0.448 0.000 0.536 0.000 0.016
#&gt; SRR1946638     3  0.4748     -1.000 0.492 0.000 0.492 0.000 0.016
#&gt; SRR1946637     3  0.4748     -1.000 0.492 0.000 0.492 0.000 0.016
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.0622     0.8160 0.000 0.012 0.980 0.000 0.008 0.000
#&gt; SRR1946691     6  0.3371     0.8540 0.000 0.292 0.000 0.000 0.000 0.708
#&gt; SRR1946690     2  0.2191     0.7480 0.000 0.876 0.000 0.000 0.004 0.120
#&gt; SRR1946689     1  0.6243    -0.0256 0.448 0.012 0.000 0.252 0.000 0.288
#&gt; SRR1946686     3  0.0964     0.8148 0.004 0.012 0.968 0.000 0.016 0.000
#&gt; SRR1946685     5  0.3601     0.4931 0.000 0.312 0.000 0.000 0.684 0.004
#&gt; SRR1946688     6  0.3351     0.8519 0.000 0.288 0.000 0.000 0.000 0.712
#&gt; SRR1946684     5  0.0000     0.7817 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946683     5  0.0713     0.7861 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1946682     6  0.4435     0.8300 0.000 0.264 0.000 0.000 0.064 0.672
#&gt; SRR1946680     3  0.5644    -0.0669 0.000 0.424 0.456 0.112 0.004 0.004
#&gt; SRR1946681     2  0.3087     0.8065 0.000 0.864 0.064 0.040 0.028 0.004
#&gt; SRR1946687     3  0.0000     0.8100 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946679     2  0.1327     0.8927 0.000 0.936 0.000 0.000 0.064 0.000
#&gt; SRR1946678     5  0.4495     0.3483 0.064 0.000 0.276 0.000 0.660 0.000
#&gt; SRR1946676     2  0.1327     0.8927 0.000 0.936 0.000 0.000 0.064 0.000
#&gt; SRR1946677     5  0.5516     0.2397 0.000 0.244 0.000 0.000 0.560 0.196
#&gt; SRR1946672     3  0.2730     0.6562 0.000 0.012 0.836 0.152 0.000 0.000
#&gt; SRR1946673     5  0.0458     0.7854 0.000 0.016 0.000 0.000 0.984 0.000
#&gt; SRR1946671     5  0.0713     0.7861 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1946669     5  0.0146     0.7792 0.004 0.000 0.000 0.000 0.996 0.000
#&gt; SRR1946668     5  0.0000     0.7817 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946666     3  0.0000     0.8100 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946667     1  0.6243    -0.0256 0.448 0.012 0.000 0.252 0.000 0.288
#&gt; SRR1946670     6  0.5673     0.5548 0.000 0.356 0.000 0.000 0.164 0.480
#&gt; SRR1946663     6  0.3390     0.8545 0.000 0.296 0.000 0.000 0.000 0.704
#&gt; SRR1946664     2  0.2191     0.7480 0.000 0.876 0.000 0.000 0.004 0.120
#&gt; SRR1946662     5  0.2092     0.7283 0.000 0.124 0.000 0.000 0.876 0.000
#&gt; SRR1946661     6  0.5255     0.7443 0.000 0.272 0.000 0.000 0.140 0.588
#&gt; SRR1946660     6  0.3351     0.8519 0.000 0.288 0.000 0.000 0.000 0.712
#&gt; SRR1946659     3  0.0260     0.8131 0.000 0.008 0.992 0.000 0.000 0.000
#&gt; SRR1946658     2  0.2917     0.8434 0.000 0.852 0.004 0.000 0.104 0.040
#&gt; SRR1946657     2  0.1327     0.8927 0.000 0.936 0.000 0.000 0.064 0.000
#&gt; SRR1946655     4  0.3265     1.0000 0.000 0.004 0.248 0.748 0.000 0.000
#&gt; SRR1946654     3  0.1237     0.8105 0.000 0.020 0.956 0.004 0.020 0.000
#&gt; SRR1946653     3  0.0000     0.8100 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946652     2  0.1863     0.8624 0.000 0.896 0.000 0.000 0.104 0.000
#&gt; SRR1946651     2  0.1531     0.8916 0.000 0.928 0.000 0.000 0.068 0.004
#&gt; SRR1946650     6  0.4291     0.8377 0.000 0.268 0.000 0.000 0.052 0.680
#&gt; SRR1946649     5  0.3050     0.6078 0.000 0.236 0.000 0.000 0.764 0.000
#&gt; SRR1946648     3  0.2883     0.5801 0.000 0.000 0.788 0.000 0.212 0.000
#&gt; SRR1946647     5  0.0260     0.7838 0.000 0.008 0.000 0.000 0.992 0.000
#&gt; SRR1946646     3  0.2309     0.7508 0.000 0.028 0.888 0.000 0.084 0.000
#&gt; SRR1946645     5  0.1957     0.7415 0.000 0.112 0.000 0.000 0.888 0.000
#&gt; SRR1946644     5  0.5424     0.3711 0.000 0.264 0.024 0.000 0.612 0.100
#&gt; SRR1946643     4  0.3265     1.0000 0.000 0.004 0.248 0.748 0.000 0.000
#&gt; SRR1946642     5  0.4587     0.3078 0.064 0.000 0.296 0.000 0.640 0.000
#&gt; SRR1946641     1  0.4062     0.5632 0.552 0.000 0.440 0.000 0.008 0.000
#&gt; SRR1946656     4  0.3265     1.0000 0.000 0.004 0.248 0.748 0.000 0.000
#&gt; SRR1946640     1  0.4062     0.5632 0.552 0.000 0.440 0.000 0.008 0.000
#&gt; SRR1946639     1  0.4062     0.5632 0.552 0.000 0.440 0.000 0.008 0.000
#&gt; SRR1946638     1  0.4062     0.5632 0.552 0.000 0.440 0.000 0.008 0.000
#&gt; SRR1946637     1  0.4062     0.5632 0.552 0.000 0.440 0.000 0.008 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.720           0.885       0.932          0.499 0.495   0.495
#> 3 3 0.607           0.748       0.857          0.328 0.718   0.491
#> 4 4 0.577           0.712       0.829          0.138 0.739   0.371
#> 5 5 0.746           0.640       0.838          0.067 0.819   0.415
#> 6 6 0.861           0.793       0.900          0.046 0.898   0.554
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1  0.2603      0.924 0.956 0.044
#&gt; SRR1946691     2  0.2236      0.925 0.036 0.964
#&gt; SRR1946690     2  0.0376      0.921 0.004 0.996
#&gt; SRR1946689     2  0.4298      0.898 0.088 0.912
#&gt; SRR1946686     1  0.2603      0.924 0.956 0.044
#&gt; SRR1946685     1  0.9933      0.174 0.548 0.452
#&gt; SRR1946688     2  0.2423      0.925 0.040 0.960
#&gt; SRR1946684     2  0.4939      0.915 0.108 0.892
#&gt; SRR1946683     2  0.6438      0.843 0.164 0.836
#&gt; SRR1946682     2  0.2603      0.924 0.044 0.956
#&gt; SRR1946680     2  0.6623      0.825 0.172 0.828
#&gt; SRR1946681     2  0.4562      0.901 0.096 0.904
#&gt; SRR1946687     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946679     2  0.3114      0.921 0.056 0.944
#&gt; SRR1946678     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946676     2  0.4431      0.903 0.092 0.908
#&gt; SRR1946677     2  0.2603      0.924 0.044 0.956
#&gt; SRR1946672     1  0.2603      0.924 0.956 0.044
#&gt; SRR1946673     2  0.4815      0.916 0.104 0.896
#&gt; SRR1946671     2  0.8016      0.773 0.244 0.756
#&gt; SRR1946669     1  0.7674      0.685 0.776 0.224
#&gt; SRR1946668     2  0.4298      0.910 0.088 0.912
#&gt; SRR1946666     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946667     2  0.8763      0.590 0.296 0.704
#&gt; SRR1946670     2  0.0672      0.924 0.008 0.992
#&gt; SRR1946663     2  0.2603      0.924 0.044 0.956
#&gt; SRR1946664     2  0.0376      0.921 0.004 0.996
#&gt; SRR1946662     2  0.3879      0.919 0.076 0.924
#&gt; SRR1946661     2  0.2603      0.924 0.044 0.956
#&gt; SRR1946660     2  0.2423      0.925 0.040 0.960
#&gt; SRR1946659     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946658     2  0.0376      0.921 0.004 0.996
#&gt; SRR1946657     2  0.3114      0.921 0.056 0.944
#&gt; SRR1946655     1  0.2603      0.924 0.956 0.044
#&gt; SRR1946654     1  0.2603      0.924 0.956 0.044
#&gt; SRR1946653     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946652     2  0.1633      0.925 0.024 0.976
#&gt; SRR1946651     2  0.1843      0.925 0.028 0.972
#&gt; SRR1946650     2  0.2603      0.924 0.044 0.956
#&gt; SRR1946649     2  0.4562      0.910 0.096 0.904
#&gt; SRR1946648     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946647     1  0.3879      0.881 0.924 0.076
#&gt; SRR1946646     1  0.2603      0.924 0.956 0.044
#&gt; SRR1946645     1  0.8386      0.600 0.732 0.268
#&gt; SRR1946644     2  0.2236      0.926 0.036 0.964
#&gt; SRR1946643     1  0.2603      0.924 0.956 0.044
#&gt; SRR1946642     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946641     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946656     1  0.2603      0.924 0.956 0.044
#&gt; SRR1946640     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946639     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946638     1  0.0376      0.932 0.996 0.004
#&gt; SRR1946637     1  0.0376      0.932 0.996 0.004
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.4605     0.7270 0.204 0.000 0.796
#&gt; SRR1946691     2  0.0424     0.8149 0.000 0.992 0.008
#&gt; SRR1946690     2  0.4235     0.8101 0.000 0.824 0.176
#&gt; SRR1946689     3  0.5254     0.6657 0.000 0.264 0.736
#&gt; SRR1946686     1  0.4654     0.6599 0.792 0.000 0.208
#&gt; SRR1946685     3  0.7337    -0.2427 0.032 0.428 0.540
#&gt; SRR1946688     2  0.0424     0.8149 0.000 0.992 0.008
#&gt; SRR1946684     1  0.8159     0.2980 0.588 0.320 0.092
#&gt; SRR1946683     2  0.7542     0.7508 0.120 0.688 0.192
#&gt; SRR1946682     2  0.0424     0.8149 0.000 0.992 0.008
#&gt; SRR1946680     3  0.2846     0.7816 0.020 0.056 0.924
#&gt; SRR1946681     3  0.5988     0.0337 0.000 0.368 0.632
#&gt; SRR1946687     3  0.5327     0.6583 0.272 0.000 0.728
#&gt; SRR1946679     2  0.5254     0.7938 0.000 0.736 0.264
#&gt; SRR1946678     1  0.0000     0.9094 1.000 0.000 0.000
#&gt; SRR1946676     2  0.5327     0.7878 0.000 0.728 0.272
#&gt; SRR1946677     2  0.0000     0.8163 0.000 1.000 0.000
#&gt; SRR1946672     3  0.3816     0.7637 0.148 0.000 0.852
#&gt; SRR1946673     2  0.7884     0.6777 0.224 0.656 0.120
#&gt; SRR1946671     2  0.7919     0.4088 0.380 0.556 0.064
#&gt; SRR1946669     1  0.2651     0.8686 0.928 0.012 0.060
#&gt; SRR1946668     1  0.4953     0.7620 0.808 0.176 0.016
#&gt; SRR1946666     1  0.0000     0.9094 1.000 0.000 0.000
#&gt; SRR1946667     3  0.5254     0.6657 0.000 0.264 0.736
#&gt; SRR1946670     2  0.0424     0.8149 0.000 0.992 0.008
#&gt; SRR1946663     2  0.0424     0.8149 0.000 0.992 0.008
#&gt; SRR1946664     2  0.5178     0.7977 0.000 0.744 0.256
#&gt; SRR1946662     2  0.6722     0.7874 0.060 0.720 0.220
#&gt; SRR1946661     2  0.0237     0.8159 0.000 0.996 0.004
#&gt; SRR1946660     2  0.0424     0.8149 0.000 0.992 0.008
#&gt; SRR1946659     1  0.0892     0.8955 0.980 0.000 0.020
#&gt; SRR1946658     2  0.2448     0.8209 0.000 0.924 0.076
#&gt; SRR1946657     2  0.5254     0.7938 0.000 0.736 0.264
#&gt; SRR1946655     3  0.2165     0.7896 0.064 0.000 0.936
#&gt; SRR1946654     3  0.2711     0.7863 0.088 0.000 0.912
#&gt; SRR1946653     3  0.5327     0.6583 0.272 0.000 0.728
#&gt; SRR1946652     2  0.5254     0.7938 0.000 0.736 0.264
#&gt; SRR1946651     2  0.5254     0.7938 0.000 0.736 0.264
#&gt; SRR1946650     2  0.0237     0.8159 0.000 0.996 0.004
#&gt; SRR1946649     2  0.5698     0.7960 0.012 0.736 0.252
#&gt; SRR1946648     3  0.5678     0.6039 0.316 0.000 0.684
#&gt; SRR1946647     1  0.2173     0.8811 0.944 0.008 0.048
#&gt; SRR1946646     3  0.2165     0.7893 0.064 0.000 0.936
#&gt; SRR1946645     1  0.2903     0.8764 0.924 0.048 0.028
#&gt; SRR1946644     3  0.0592     0.7595 0.000 0.012 0.988
#&gt; SRR1946643     3  0.0747     0.7742 0.016 0.000 0.984
#&gt; SRR1946642     1  0.0000     0.9094 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.9094 1.000 0.000 0.000
#&gt; SRR1946656     3  0.2066     0.7887 0.060 0.000 0.940
#&gt; SRR1946640     1  0.0000     0.9094 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.9094 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9094 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9094 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.3577      0.814 0.012 0.156 0.832 0.000
#&gt; SRR1946691     4  0.0336      0.788 0.008 0.000 0.000 0.992
#&gt; SRR1946690     4  0.4998     -0.203 0.000 0.488 0.000 0.512
#&gt; SRR1946689     4  0.3400      0.665 0.000 0.000 0.180 0.820
#&gt; SRR1946686     3  0.3708      0.813 0.020 0.148 0.832 0.000
#&gt; SRR1946685     2  0.0000      0.766 0.000 1.000 0.000 0.000
#&gt; SRR1946688     4  0.1716      0.755 0.000 0.000 0.064 0.936
#&gt; SRR1946684     1  0.3123      0.713 0.844 0.000 0.000 0.156
#&gt; SRR1946683     1  0.6340      0.607 0.712 0.056 0.064 0.168
#&gt; SRR1946682     4  0.2760      0.768 0.128 0.000 0.000 0.872
#&gt; SRR1946680     3  0.4827      0.781 0.000 0.124 0.784 0.092
#&gt; SRR1946681     2  0.1792      0.704 0.000 0.932 0.068 0.000
#&gt; SRR1946687     3  0.1389      0.780 0.000 0.000 0.952 0.048
#&gt; SRR1946679     2  0.0469      0.774 0.000 0.988 0.000 0.012
#&gt; SRR1946678     1  0.2149      0.816 0.912 0.000 0.088 0.000
#&gt; SRR1946676     2  0.0000      0.766 0.000 1.000 0.000 0.000
#&gt; SRR1946677     4  0.4454      0.571 0.308 0.000 0.000 0.692
#&gt; SRR1946672     3  0.3311      0.814 0.000 0.172 0.828 0.000
#&gt; SRR1946673     1  0.6400      0.476 0.652 0.180 0.000 0.168
#&gt; SRR1946671     1  0.4004      0.687 0.812 0.024 0.000 0.164
#&gt; SRR1946669     1  0.0000      0.814 1.000 0.000 0.000 0.000
#&gt; SRR1946668     1  0.2081      0.777 0.916 0.000 0.000 0.084
#&gt; SRR1946666     3  0.3486      0.704 0.188 0.000 0.812 0.000
#&gt; SRR1946667     4  0.4605      0.469 0.000 0.000 0.336 0.664
#&gt; SRR1946670     4  0.0188      0.786 0.004 0.000 0.000 0.996
#&gt; SRR1946663     4  0.2149      0.785 0.088 0.000 0.000 0.912
#&gt; SRR1946664     2  0.3266      0.767 0.000 0.832 0.000 0.168
#&gt; SRR1946662     2  0.6503      0.596 0.196 0.640 0.000 0.164
#&gt; SRR1946661     4  0.2345      0.782 0.100 0.000 0.000 0.900
#&gt; SRR1946660     4  0.1302      0.792 0.044 0.000 0.000 0.956
#&gt; SRR1946659     3  0.4356      0.548 0.292 0.000 0.708 0.000
#&gt; SRR1946658     2  0.4989      0.244 0.000 0.528 0.000 0.472
#&gt; SRR1946657     2  0.2530      0.790 0.000 0.888 0.000 0.112
#&gt; SRR1946655     3  0.4356      0.773 0.000 0.292 0.708 0.000
#&gt; SRR1946654     3  0.4040      0.797 0.000 0.248 0.752 0.000
#&gt; SRR1946653     3  0.1716      0.773 0.000 0.000 0.936 0.064
#&gt; SRR1946652     2  0.3024      0.781 0.000 0.852 0.000 0.148
#&gt; SRR1946651     2  0.2973      0.783 0.000 0.856 0.000 0.144
#&gt; SRR1946650     4  0.4300      0.724 0.092 0.088 0.000 0.820
#&gt; SRR1946649     2  0.6473      0.601 0.188 0.644 0.000 0.168
#&gt; SRR1946648     3  0.4160      0.734 0.168 0.008 0.808 0.016
#&gt; SRR1946647     1  0.0000      0.814 1.000 0.000 0.000 0.000
#&gt; SRR1946646     3  0.4292      0.743 0.000 0.100 0.820 0.080
#&gt; SRR1946645     1  0.2282      0.793 0.924 0.000 0.024 0.052
#&gt; SRR1946644     2  0.4707      0.671 0.000 0.760 0.204 0.036
#&gt; SRR1946643     3  0.4661      0.718 0.000 0.348 0.652 0.000
#&gt; SRR1946642     1  0.2081      0.816 0.916 0.000 0.084 0.000
#&gt; SRR1946641     1  0.3266      0.792 0.832 0.000 0.168 0.000
#&gt; SRR1946656     3  0.4500      0.752 0.000 0.316 0.684 0.000
#&gt; SRR1946640     1  0.3266      0.792 0.832 0.000 0.168 0.000
#&gt; SRR1946639     1  0.3266      0.792 0.832 0.000 0.168 0.000
#&gt; SRR1946638     1  0.3266      0.792 0.832 0.000 0.168 0.000
#&gt; SRR1946637     1  0.3266      0.792 0.832 0.000 0.168 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.0162     0.8298 0.004 0.000 0.996 0.000 0.000
#&gt; SRR1946691     4  0.6182     0.2899 0.000 0.324 0.000 0.520 0.156
#&gt; SRR1946690     2  0.1800     0.8124 0.000 0.932 0.000 0.048 0.020
#&gt; SRR1946689     4  0.0880     0.6588 0.000 0.000 0.032 0.968 0.000
#&gt; SRR1946686     3  0.0794     0.8295 0.028 0.000 0.972 0.000 0.000
#&gt; SRR1946685     2  0.0693     0.8488 0.012 0.980 0.008 0.000 0.000
#&gt; SRR1946688     4  0.2997     0.6021 0.000 0.012 0.000 0.840 0.148
#&gt; SRR1946684     5  0.3532     0.6806 0.128 0.048 0.000 0.000 0.824
#&gt; SRR1946683     5  0.0880     0.6988 0.000 0.000 0.032 0.000 0.968
#&gt; SRR1946682     5  0.4455     0.2325 0.000 0.008 0.000 0.404 0.588
#&gt; SRR1946680     3  0.0880     0.8115 0.000 0.000 0.968 0.032 0.000
#&gt; SRR1946681     3  0.4273     0.1659 0.000 0.448 0.552 0.000 0.000
#&gt; SRR1946687     3  0.4803     0.1030 0.020 0.000 0.536 0.444 0.000
#&gt; SRR1946679     2  0.0609     0.8485 0.000 0.980 0.020 0.000 0.000
#&gt; SRR1946678     5  0.4306     0.0507 0.492 0.000 0.000 0.000 0.508
#&gt; SRR1946676     2  0.0609     0.8482 0.000 0.980 0.020 0.000 0.000
#&gt; SRR1946677     5  0.0162     0.6988 0.000 0.000 0.000 0.004 0.996
#&gt; SRR1946672     3  0.0992     0.8324 0.024 0.008 0.968 0.000 0.000
#&gt; SRR1946673     5  0.3656     0.6423 0.032 0.168 0.000 0.000 0.800
#&gt; SRR1946671     5  0.0771     0.7065 0.020 0.000 0.004 0.000 0.976
#&gt; SRR1946669     5  0.3109     0.6408 0.200 0.000 0.000 0.000 0.800
#&gt; SRR1946668     5  0.1197     0.7080 0.048 0.000 0.000 0.000 0.952
#&gt; SRR1946666     3  0.1792     0.7966 0.084 0.000 0.916 0.000 0.000
#&gt; SRR1946667     4  0.0880     0.6588 0.000 0.000 0.032 0.968 0.000
#&gt; SRR1946670     4  0.2585     0.6492 0.000 0.024 0.008 0.896 0.072
#&gt; SRR1946663     5  0.4440     0.0908 0.000 0.004 0.000 0.468 0.528
#&gt; SRR1946664     2  0.0404     0.8470 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1946662     5  0.3430     0.5913 0.000 0.220 0.004 0.000 0.776
#&gt; SRR1946661     5  0.4624     0.3290 0.000 0.024 0.000 0.340 0.636
#&gt; SRR1946660     4  0.4402     0.5333 0.000 0.056 0.000 0.740 0.204
#&gt; SRR1946659     1  0.0290     0.9847 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1946658     2  0.6462     0.3392 0.000 0.568 0.016 0.196 0.220
#&gt; SRR1946657     2  0.0162     0.8512 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1946655     3  0.0794     0.8346 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1946654     3  0.0955     0.8345 0.004 0.028 0.968 0.000 0.000
#&gt; SRR1946653     4  0.5236    -0.1217 0.044 0.000 0.464 0.492 0.000
#&gt; SRR1946652     2  0.0955     0.8428 0.000 0.968 0.004 0.000 0.028
#&gt; SRR1946651     2  0.0000     0.8509 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946650     5  0.6610    -0.0574 0.000 0.220 0.000 0.352 0.428
#&gt; SRR1946649     2  0.4829     0.0836 0.000 0.496 0.000 0.020 0.484
#&gt; SRR1946648     3  0.5333     0.4412 0.004 0.000 0.628 0.068 0.300
#&gt; SRR1946647     5  0.2561     0.6852 0.144 0.000 0.000 0.000 0.856
#&gt; SRR1946646     4  0.6920     0.2299 0.016 0.300 0.216 0.468 0.000
#&gt; SRR1946645     5  0.0671     0.7030 0.016 0.000 0.000 0.004 0.980
#&gt; SRR1946644     2  0.2660     0.7411 0.000 0.864 0.008 0.128 0.000
#&gt; SRR1946643     3  0.0794     0.8346 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1946642     1  0.0290     0.9930 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1946641     1  0.0162     0.9967 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946656     3  0.0794     0.8346 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1946640     1  0.0162     0.9967 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946639     1  0.0162     0.9967 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946638     1  0.0162     0.9967 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946637     1  0.0162     0.9967 0.996 0.000 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.0632     0.9062 0.000 0.000 0.976 0.024 0.000 0.000
#&gt; SRR1946691     6  0.2633     0.7611 0.000 0.104 0.000 0.032 0.000 0.864
#&gt; SRR1946690     2  0.3841     0.5583 0.000 0.716 0.000 0.028 0.000 0.256
#&gt; SRR1946689     4  0.1524     0.8482 0.000 0.000 0.008 0.932 0.000 0.060
#&gt; SRR1946686     3  0.0767     0.9038 0.008 0.004 0.976 0.012 0.000 0.000
#&gt; SRR1946685     2  0.0508     0.8596 0.000 0.984 0.004 0.012 0.000 0.000
#&gt; SRR1946688     6  0.1141     0.8343 0.000 0.000 0.000 0.052 0.000 0.948
#&gt; SRR1946684     5  0.0000     0.8570 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946683     5  0.4252     0.6473 0.000 0.004 0.052 0.008 0.736 0.200
#&gt; SRR1946682     6  0.0692     0.8525 0.000 0.000 0.000 0.004 0.020 0.976
#&gt; SRR1946680     3  0.3737     0.2988 0.000 0.000 0.608 0.392 0.000 0.000
#&gt; SRR1946681     3  0.3277     0.7188 0.000 0.188 0.792 0.016 0.004 0.000
#&gt; SRR1946687     4  0.1753     0.8277 0.004 0.000 0.084 0.912 0.000 0.000
#&gt; SRR1946679     2  0.1059     0.8544 0.000 0.964 0.016 0.016 0.004 0.000
#&gt; SRR1946678     5  0.0363     0.8518 0.012 0.000 0.000 0.000 0.988 0.000
#&gt; SRR1946676     2  0.0820     0.8572 0.000 0.972 0.012 0.016 0.000 0.000
#&gt; SRR1946677     6  0.2163     0.8066 0.000 0.000 0.004 0.008 0.096 0.892
#&gt; SRR1946672     3  0.0291     0.9104 0.000 0.004 0.992 0.004 0.000 0.000
#&gt; SRR1946673     5  0.0000     0.8570 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946671     5  0.4256     0.4578 0.000 0.008 0.008 0.008 0.648 0.328
#&gt; SRR1946669     5  0.0146     0.8566 0.004 0.000 0.000 0.000 0.996 0.000
#&gt; SRR1946668     5  0.0146     0.8566 0.004 0.000 0.000 0.000 0.996 0.000
#&gt; SRR1946666     3  0.1232     0.9004 0.016 0.000 0.956 0.024 0.000 0.004
#&gt; SRR1946667     4  0.1500     0.8508 0.000 0.000 0.012 0.936 0.000 0.052
#&gt; SRR1946670     4  0.4691     0.6602 0.000 0.012 0.004 0.684 0.056 0.244
#&gt; SRR1946663     6  0.0458     0.8491 0.000 0.000 0.000 0.016 0.000 0.984
#&gt; SRR1946664     2  0.0632     0.8564 0.000 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1946662     5  0.0146     0.8549 0.000 0.000 0.000 0.004 0.996 0.000
#&gt; SRR1946661     6  0.0622     0.8528 0.000 0.008 0.000 0.000 0.012 0.980
#&gt; SRR1946660     6  0.0458     0.8491 0.000 0.000 0.000 0.016 0.000 0.984
#&gt; SRR1946659     1  0.0146     0.9911 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR1946658     2  0.6217     0.3881 0.000 0.524 0.024 0.092 0.332 0.028
#&gt; SRR1946657     2  0.0632     0.8564 0.000 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1946655     3  0.0146     0.9117 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1946654     3  0.0777     0.9075 0.000 0.004 0.972 0.024 0.000 0.000
#&gt; SRR1946653     4  0.2350     0.8266 0.036 0.000 0.076 0.888 0.000 0.000
#&gt; SRR1946652     2  0.3354     0.7274 0.000 0.792 0.008 0.016 0.184 0.000
#&gt; SRR1946651     2  0.0000     0.8597 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946650     6  0.0790     0.8487 0.000 0.032 0.000 0.000 0.000 0.968
#&gt; SRR1946649     6  0.5828     0.0342 0.000 0.436 0.004 0.012 0.112 0.436
#&gt; SRR1946648     5  0.6246     0.0187 0.000 0.004 0.156 0.380 0.440 0.020
#&gt; SRR1946647     5  0.0000     0.8570 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946646     4  0.3534     0.6368 0.000 0.244 0.016 0.740 0.000 0.000
#&gt; SRR1946645     6  0.3523     0.6625 0.004 0.004 0.004 0.008 0.208 0.772
#&gt; SRR1946644     2  0.1610     0.8220 0.000 0.916 0.000 0.084 0.000 0.000
#&gt; SRR1946643     3  0.0291     0.9122 0.000 0.004 0.992 0.004 0.000 0.000
#&gt; SRR1946642     1  0.0146     0.9985 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1946641     1  0.0146     0.9985 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1946656     3  0.0291     0.9122 0.000 0.004 0.992 0.004 0.000 0.000
#&gt; SRR1946640     1  0.0146     0.9985 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1946639     1  0.0146     0.9985 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1946638     1  0.0146     0.9985 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1946637     1  0.0146     0.9985 0.996 0.000 0.000 0.000 0.004 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.322           0.847       0.822         0.3312 0.713   0.713
#> 3 3 0.365           0.721       0.836         0.6424 0.708   0.590
#> 4 4 0.525           0.677       0.798         0.2737 0.848   0.637
#> 5 5 0.594           0.690       0.816         0.0433 0.987   0.951
#> 6 6 0.710           0.576       0.743         0.0926 0.814   0.430
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1   0.584      0.839 0.860 0.140
#&gt; SRR1946691     2   0.563      0.952 0.132 0.868
#&gt; SRR1946690     2   0.563      0.952 0.132 0.868
#&gt; SRR1946689     2   0.416      0.930 0.084 0.916
#&gt; SRR1946686     1   0.584      0.839 0.860 0.140
#&gt; SRR1946685     1   0.714      0.821 0.804 0.196
#&gt; SRR1946688     1   0.662      0.837 0.828 0.172
#&gt; SRR1946684     1   0.311      0.831 0.944 0.056
#&gt; SRR1946683     1   0.163      0.856 0.976 0.024
#&gt; SRR1946682     1   0.662      0.837 0.828 0.172
#&gt; SRR1946680     2   0.416      0.930 0.084 0.916
#&gt; SRR1946681     2   0.662      0.927 0.172 0.828
#&gt; SRR1946687     1   0.584      0.839 0.860 0.140
#&gt; SRR1946679     1   0.714      0.821 0.804 0.196
#&gt; SRR1946678     1   0.416      0.814 0.916 0.084
#&gt; SRR1946676     1   0.506      0.859 0.888 0.112
#&gt; SRR1946677     1   0.163      0.856 0.976 0.024
#&gt; SRR1946672     1   0.595      0.837 0.856 0.144
#&gt; SRR1946673     1   0.311      0.831 0.944 0.056
#&gt; SRR1946671     1   0.224      0.857 0.964 0.036
#&gt; SRR1946669     1   0.416      0.814 0.916 0.084
#&gt; SRR1946668     1   0.311      0.831 0.944 0.056
#&gt; SRR1946666     1   0.584      0.839 0.860 0.140
#&gt; SRR1946667     2   0.416      0.930 0.084 0.916
#&gt; SRR1946670     1   0.662      0.837 0.828 0.172
#&gt; SRR1946663     1   0.662      0.837 0.828 0.172
#&gt; SRR1946664     2   0.563      0.952 0.132 0.868
#&gt; SRR1946662     1   0.311      0.831 0.944 0.056
#&gt; SRR1946661     1   0.311      0.852 0.944 0.056
#&gt; SRR1946660     1   0.662      0.837 0.828 0.172
#&gt; SRR1946659     1   0.584      0.839 0.860 0.140
#&gt; SRR1946658     1   0.662      0.837 0.828 0.172
#&gt; SRR1946657     1   0.714      0.821 0.804 0.196
#&gt; SRR1946655     1   0.925      0.613 0.660 0.340
#&gt; SRR1946654     1   0.706      0.806 0.808 0.192
#&gt; SRR1946653     1   0.584      0.839 0.860 0.140
#&gt; SRR1946652     1   0.714      0.821 0.804 0.196
#&gt; SRR1946651     1   0.714      0.821 0.804 0.196
#&gt; SRR1946650     1   0.443      0.853 0.908 0.092
#&gt; SRR1946649     1   0.278      0.858 0.952 0.048
#&gt; SRR1946648     1   0.416      0.858 0.916 0.084
#&gt; SRR1946647     1   0.311      0.831 0.944 0.056
#&gt; SRR1946646     1   0.714      0.821 0.804 0.196
#&gt; SRR1946645     1   0.163      0.856 0.976 0.024
#&gt; SRR1946644     1   0.714      0.821 0.804 0.196
#&gt; SRR1946643     2   0.662      0.927 0.172 0.828
#&gt; SRR1946642     1   0.416      0.814 0.916 0.084
#&gt; SRR1946641     1   0.416      0.814 0.916 0.084
#&gt; SRR1946656     2   0.662      0.927 0.172 0.828
#&gt; SRR1946640     1   0.416      0.814 0.916 0.084
#&gt; SRR1946639     1   0.416      0.814 0.916 0.084
#&gt; SRR1946638     1   0.416      0.814 0.916 0.084
#&gt; SRR1946637     1   0.416      0.814 0.916 0.084
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     2  0.7136      0.722 0.212 0.704 0.084
#&gt; SRR1946691     3  0.5678      0.819 0.000 0.316 0.684
#&gt; SRR1946690     3  0.5678      0.819 0.000 0.316 0.684
#&gt; SRR1946689     3  0.0424      0.733 0.000 0.008 0.992
#&gt; SRR1946686     2  0.7136      0.722 0.212 0.704 0.084
#&gt; SRR1946685     2  0.0424      0.805 0.000 0.992 0.008
#&gt; SRR1946688     2  0.1031      0.815 0.024 0.976 0.000
#&gt; SRR1946684     1  0.6095      0.413 0.608 0.392 0.000
#&gt; SRR1946683     2  0.5363      0.672 0.276 0.724 0.000
#&gt; SRR1946682     2  0.1031      0.815 0.024 0.976 0.000
#&gt; SRR1946680     3  0.0424      0.733 0.000 0.008 0.992
#&gt; SRR1946681     3  0.5363      0.821 0.000 0.276 0.724
#&gt; SRR1946687     2  0.7136      0.722 0.212 0.704 0.084
#&gt; SRR1946679     2  0.0424      0.805 0.000 0.992 0.008
#&gt; SRR1946678     1  0.0000      0.734 1.000 0.000 0.000
#&gt; SRR1946676     2  0.3193      0.807 0.100 0.896 0.004
#&gt; SRR1946677     2  0.5363      0.666 0.276 0.724 0.000
#&gt; SRR1946672     2  0.7169      0.723 0.208 0.704 0.088
#&gt; SRR1946673     1  0.6111      0.402 0.604 0.396 0.000
#&gt; SRR1946671     2  0.4346      0.747 0.184 0.816 0.000
#&gt; SRR1946669     1  0.3267      0.710 0.884 0.116 0.000
#&gt; SRR1946668     1  0.6095      0.413 0.608 0.392 0.000
#&gt; SRR1946666     2  0.7136      0.722 0.212 0.704 0.084
#&gt; SRR1946667     3  0.0424      0.733 0.000 0.008 0.992
#&gt; SRR1946670     2  0.1031      0.815 0.024 0.976 0.000
#&gt; SRR1946663     2  0.1031      0.815 0.024 0.976 0.000
#&gt; SRR1946664     3  0.5678      0.819 0.000 0.316 0.684
#&gt; SRR1946662     1  0.6111      0.402 0.604 0.396 0.000
#&gt; SRR1946661     2  0.6045      0.396 0.380 0.620 0.000
#&gt; SRR1946660     2  0.1031      0.815 0.024 0.976 0.000
#&gt; SRR1946659     2  0.7136      0.722 0.212 0.704 0.084
#&gt; SRR1946658     2  0.1031      0.815 0.024 0.976 0.000
#&gt; SRR1946657     2  0.0424      0.805 0.000 0.992 0.008
#&gt; SRR1946655     2  0.4974      0.651 0.000 0.764 0.236
#&gt; SRR1946654     2  0.6910      0.744 0.144 0.736 0.120
#&gt; SRR1946653     2  0.7136      0.722 0.212 0.704 0.084
#&gt; SRR1946652     2  0.0424      0.805 0.000 0.992 0.008
#&gt; SRR1946651     2  0.0424      0.805 0.000 0.992 0.008
#&gt; SRR1946650     2  0.3192      0.785 0.112 0.888 0.000
#&gt; SRR1946649     2  0.4002      0.764 0.160 0.840 0.000
#&gt; SRR1946648     2  0.6067      0.717 0.236 0.736 0.028
#&gt; SRR1946647     1  0.6095      0.413 0.608 0.392 0.000
#&gt; SRR1946646     2  0.0424      0.805 0.000 0.992 0.008
#&gt; SRR1946645     2  0.5397      0.665 0.280 0.720 0.000
#&gt; SRR1946644     2  0.0424      0.805 0.000 0.992 0.008
#&gt; SRR1946643     3  0.5363      0.821 0.000 0.276 0.724
#&gt; SRR1946642     1  0.0000      0.734 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000      0.734 1.000 0.000 0.000
#&gt; SRR1946656     3  0.5363      0.821 0.000 0.276 0.724
#&gt; SRR1946640     1  0.0000      0.734 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.734 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.734 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.734 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.4595    0.90319 0.184 0.040 0.776 0.000
#&gt; SRR1946691     4  0.6690    0.74179 0.000 0.248 0.144 0.608
#&gt; SRR1946690     4  0.6690    0.74179 0.000 0.248 0.144 0.608
#&gt; SRR1946689     4  0.0000    0.73194 0.000 0.000 0.000 1.000
#&gt; SRR1946686     3  0.4595    0.90319 0.184 0.040 0.776 0.000
#&gt; SRR1946685     2  0.2011    0.77020 0.000 0.920 0.080 0.000
#&gt; SRR1946688     2  0.1389    0.78795 0.000 0.952 0.048 0.000
#&gt; SRR1946684     1  0.4866    0.45763 0.596 0.404 0.000 0.000
#&gt; SRR1946683     2  0.7776   -0.03105 0.248 0.412 0.340 0.000
#&gt; SRR1946682     2  0.1389    0.78795 0.000 0.952 0.048 0.000
#&gt; SRR1946680     4  0.0000    0.73194 0.000 0.000 0.000 1.000
#&gt; SRR1946681     4  0.5971    0.72032 0.000 0.048 0.368 0.584
#&gt; SRR1946687     3  0.4595    0.90319 0.184 0.040 0.776 0.000
#&gt; SRR1946679     2  0.2011    0.77020 0.000 0.920 0.080 0.000
#&gt; SRR1946678     1  0.0336    0.71014 0.992 0.000 0.008 0.000
#&gt; SRR1946676     2  0.3828    0.71776 0.084 0.848 0.068 0.000
#&gt; SRR1946677     2  0.7771    0.00884 0.252 0.420 0.328 0.000
#&gt; SRR1946672     3  0.4553    0.90083 0.180 0.040 0.780 0.000
#&gt; SRR1946673     1  0.4877    0.44947 0.592 0.408 0.000 0.000
#&gt; SRR1946671     2  0.3311    0.66580 0.172 0.828 0.000 0.000
#&gt; SRR1946669     1  0.2760    0.68280 0.872 0.128 0.000 0.000
#&gt; SRR1946668     1  0.4877    0.45299 0.592 0.408 0.000 0.000
#&gt; SRR1946666     3  0.4595    0.90319 0.184 0.040 0.776 0.000
#&gt; SRR1946667     4  0.0000    0.73194 0.000 0.000 0.000 1.000
#&gt; SRR1946670     2  0.1389    0.78795 0.000 0.952 0.048 0.000
#&gt; SRR1946663     2  0.1389    0.78795 0.000 0.952 0.048 0.000
#&gt; SRR1946664     4  0.6690    0.74179 0.000 0.248 0.144 0.608
#&gt; SRR1946662     1  0.4877    0.44947 0.592 0.408 0.000 0.000
#&gt; SRR1946661     2  0.4730    0.25173 0.364 0.636 0.000 0.000
#&gt; SRR1946660     2  0.1389    0.78795 0.000 0.952 0.048 0.000
#&gt; SRR1946659     3  0.4595    0.90319 0.184 0.040 0.776 0.000
#&gt; SRR1946658     2  0.1302    0.78808 0.000 0.956 0.044 0.000
#&gt; SRR1946657     2  0.2011    0.77020 0.000 0.920 0.080 0.000
#&gt; SRR1946655     3  0.2926    0.62928 0.000 0.048 0.896 0.056
#&gt; SRR1946654     3  0.4484    0.84269 0.120 0.064 0.812 0.004
#&gt; SRR1946653     3  0.4595    0.90319 0.184 0.040 0.776 0.000
#&gt; SRR1946652     2  0.1474    0.78016 0.000 0.948 0.052 0.000
#&gt; SRR1946651     2  0.1474    0.78016 0.000 0.948 0.052 0.000
#&gt; SRR1946650     2  0.2281    0.73927 0.096 0.904 0.000 0.000
#&gt; SRR1946649     2  0.3024    0.69440 0.148 0.852 0.000 0.000
#&gt; SRR1946648     3  0.7493    0.40678 0.208 0.304 0.488 0.000
#&gt; SRR1946647     1  0.4866    0.45763 0.596 0.404 0.000 0.000
#&gt; SRR1946646     2  0.2011    0.77020 0.000 0.920 0.080 0.000
#&gt; SRR1946645     2  0.7784   -0.02420 0.252 0.412 0.336 0.000
#&gt; SRR1946644     2  0.2011    0.77020 0.000 0.920 0.080 0.000
#&gt; SRR1946643     4  0.5971    0.72032 0.000 0.048 0.368 0.584
#&gt; SRR1946642     1  0.0336    0.71014 0.992 0.000 0.008 0.000
#&gt; SRR1946641     1  0.0336    0.71014 0.992 0.000 0.008 0.000
#&gt; SRR1946656     4  0.5971    0.72032 0.000 0.048 0.368 0.584
#&gt; SRR1946640     1  0.0336    0.71014 0.992 0.000 0.008 0.000
#&gt; SRR1946639     1  0.0336    0.71014 0.992 0.000 0.008 0.000
#&gt; SRR1946638     1  0.0336    0.71014 0.992 0.000 0.008 0.000
#&gt; SRR1946637     1  0.0336    0.71014 0.992 0.000 0.008 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.2329     0.8976 0.124 0.000 0.876 0.000 0.000
#&gt; SRR1946691     2  0.0992     0.7624 0.000 0.968 0.000 0.008 0.024
#&gt; SRR1946690     2  0.0992     0.7624 0.000 0.968 0.000 0.008 0.024
#&gt; SRR1946689     4  0.0000     1.0000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946686     3  0.2329     0.8976 0.124 0.000 0.876 0.000 0.000
#&gt; SRR1946685     5  0.3266     0.7482 0.000 0.200 0.004 0.000 0.796
#&gt; SRR1946688     5  0.0162     0.7558 0.000 0.004 0.000 0.000 0.996
#&gt; SRR1946684     1  0.4161     0.4491 0.608 0.000 0.000 0.000 0.392
#&gt; SRR1946683     5  0.6685     0.0188 0.236 0.000 0.380 0.000 0.384
#&gt; SRR1946682     5  0.0162     0.7558 0.000 0.004 0.000 0.000 0.996
#&gt; SRR1946680     4  0.0000     1.0000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946681     2  0.4109     0.7637 0.000 0.700 0.288 0.012 0.000
#&gt; SRR1946687     3  0.2329     0.8976 0.124 0.000 0.876 0.000 0.000
#&gt; SRR1946679     5  0.3266     0.7482 0.000 0.200 0.004 0.000 0.796
#&gt; SRR1946678     1  0.0703     0.7191 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1946676     5  0.4144     0.7126 0.084 0.032 0.068 0.000 0.816
#&gt; SRR1946677     5  0.6695     0.0597 0.240 0.000 0.368 0.000 0.392
#&gt; SRR1946672     3  0.2723     0.8909 0.124 0.012 0.864 0.000 0.000
#&gt; SRR1946673     1  0.4171     0.4408 0.604 0.000 0.000 0.000 0.396
#&gt; SRR1946671     5  0.2966     0.6629 0.184 0.000 0.000 0.000 0.816
#&gt; SRR1946669     1  0.2230     0.6961 0.884 0.000 0.000 0.000 0.116
#&gt; SRR1946668     1  0.4171     0.4443 0.604 0.000 0.000 0.000 0.396
#&gt; SRR1946666     3  0.2329     0.8976 0.124 0.000 0.876 0.000 0.000
#&gt; SRR1946667     4  0.0000     1.0000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946670     5  0.0162     0.7558 0.000 0.004 0.000 0.000 0.996
#&gt; SRR1946663     5  0.0162     0.7558 0.000 0.004 0.000 0.000 0.996
#&gt; SRR1946664     2  0.0992     0.7624 0.000 0.968 0.000 0.008 0.024
#&gt; SRR1946662     1  0.4171     0.4408 0.604 0.000 0.000 0.000 0.396
#&gt; SRR1946661     5  0.4114     0.2633 0.376 0.000 0.000 0.000 0.624
#&gt; SRR1946660     5  0.0162     0.7558 0.000 0.004 0.000 0.000 0.996
#&gt; SRR1946659     3  0.2329     0.8976 0.124 0.000 0.876 0.000 0.000
#&gt; SRR1946658     5  0.0290     0.7564 0.000 0.008 0.000 0.000 0.992
#&gt; SRR1946657     5  0.3266     0.7482 0.000 0.200 0.004 0.000 0.796
#&gt; SRR1946655     3  0.2305     0.6149 0.000 0.092 0.896 0.012 0.000
#&gt; SRR1946654     3  0.2805     0.8306 0.072 0.020 0.888 0.000 0.020
#&gt; SRR1946653     3  0.2329     0.8976 0.124 0.000 0.876 0.000 0.000
#&gt; SRR1946652     5  0.2929     0.7555 0.000 0.180 0.000 0.000 0.820
#&gt; SRR1946651     5  0.2929     0.7555 0.000 0.180 0.000 0.000 0.820
#&gt; SRR1946650     5  0.3493     0.7271 0.108 0.060 0.000 0.000 0.832
#&gt; SRR1946649     5  0.3224     0.6887 0.160 0.016 0.000 0.000 0.824
#&gt; SRR1946648     3  0.5991     0.3808 0.148 0.000 0.564 0.000 0.288
#&gt; SRR1946647     1  0.4161     0.4491 0.608 0.000 0.000 0.000 0.392
#&gt; SRR1946646     5  0.3266     0.7482 0.000 0.200 0.004 0.000 0.796
#&gt; SRR1946645     5  0.6697     0.0257 0.240 0.000 0.376 0.000 0.384
#&gt; SRR1946644     5  0.3266     0.7482 0.000 0.200 0.004 0.000 0.796
#&gt; SRR1946643     2  0.4109     0.7637 0.000 0.700 0.288 0.012 0.000
#&gt; SRR1946642     1  0.0703     0.7191 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1946641     1  0.0703     0.7191 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1946656     2  0.4109     0.7637 0.000 0.700 0.288 0.012 0.000
#&gt; SRR1946640     1  0.0703     0.7191 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1946639     1  0.0703     0.7191 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1946638     1  0.0703     0.7191 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1946637     1  0.0703     0.7191 0.976 0.000 0.024 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5    p6
#&gt; SRR1946675     3  0.0363      0.774 0.000 0.000 0.988  0 0.012 0.000
#&gt; SRR1946691     1  0.2562      0.754 0.828 0.172 0.000  0 0.000 0.000
#&gt; SRR1946690     1  0.2562      0.754 0.828 0.172 0.000  0 0.000 0.000
#&gt; SRR1946689     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946686     3  0.0363      0.774 0.000 0.000 0.988  0 0.012 0.000
#&gt; SRR1946685     2  0.4992      0.984 0.040 0.572 0.000  0 0.368 0.020
#&gt; SRR1946688     6  0.2762      0.998 0.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1946684     5  0.0000      0.409 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946683     3  0.5778      0.181 0.000 0.056 0.452  0 0.440 0.052
#&gt; SRR1946682     6  0.2762      0.998 0.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1946680     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946681     1  0.3250      0.752 0.788 0.004 0.012  0 0.000 0.196
#&gt; SRR1946687     3  0.0363      0.774 0.000 0.000 0.988  0 0.012 0.000
#&gt; SRR1946679     2  0.4992      0.984 0.040 0.572 0.000  0 0.368 0.020
#&gt; SRR1946678     5  0.4666      0.468 0.000 0.420 0.044  0 0.536 0.000
#&gt; SRR1946676     5  0.6627     -0.703 0.012 0.396 0.116  0 0.424 0.052
#&gt; SRR1946677     5  0.5866     -0.235 0.000 0.064 0.428  0 0.456 0.052
#&gt; SRR1946672     3  0.1225      0.758 0.000 0.000 0.952  0 0.012 0.036
#&gt; SRR1946673     5  0.0146      0.407 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR1946671     5  0.5391     -0.586 0.000 0.376 0.036  0 0.540 0.048
#&gt; SRR1946669     5  0.3288      0.496 0.000 0.276 0.000  0 0.724 0.000
#&gt; SRR1946668     5  0.0146      0.407 0.000 0.000 0.000  0 0.996 0.004
#&gt; SRR1946666     3  0.0363      0.774 0.000 0.000 0.988  0 0.012 0.000
#&gt; SRR1946667     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946670     6  0.2762      0.998 0.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1946663     6  0.2762      0.998 0.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1946664     1  0.2562      0.754 0.828 0.172 0.000  0 0.000 0.000
#&gt; SRR1946662     5  0.0146      0.407 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR1946661     5  0.4323     -0.108 0.000 0.188 0.028  0 0.740 0.044
#&gt; SRR1946660     6  0.2762      0.998 0.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1946659     3  0.0363      0.774 0.000 0.000 0.988  0 0.012 0.000
#&gt; SRR1946658     6  0.2823      0.989 0.000 0.204 0.000  0 0.000 0.796
#&gt; SRR1946657     2  0.4992      0.984 0.040 0.572 0.000  0 0.368 0.020
#&gt; SRR1946655     3  0.5283      0.390 0.180 0.004 0.620  0 0.000 0.196
#&gt; SRR1946654     3  0.3334      0.690 0.040 0.024 0.844  0 0.004 0.088
#&gt; SRR1946653     3  0.0363      0.774 0.000 0.000 0.988  0 0.012 0.000
#&gt; SRR1946652     2  0.4638      0.960 0.020 0.572 0.000  0 0.392 0.016
#&gt; SRR1946651     2  0.4638      0.960 0.020 0.572 0.000  0 0.392 0.016
#&gt; SRR1946650     5  0.4928     -0.717 0.004 0.444 0.000  0 0.500 0.052
#&gt; SRR1946649     5  0.5432     -0.635 0.000 0.400 0.036  0 0.516 0.048
#&gt; SRR1946648     3  0.3871      0.501 0.000 0.000 0.676  0 0.308 0.016
#&gt; SRR1946647     5  0.0000      0.409 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946646     2  0.4992      0.984 0.040 0.572 0.000  0 0.368 0.020
#&gt; SRR1946645     3  0.5779      0.172 0.000 0.056 0.448  0 0.444 0.052
#&gt; SRR1946644     2  0.4992      0.984 0.040 0.572 0.000  0 0.368 0.020
#&gt; SRR1946643     1  0.3250      0.752 0.788 0.004 0.012  0 0.000 0.196
#&gt; SRR1946642     5  0.4666      0.468 0.000 0.420 0.044  0 0.536 0.000
#&gt; SRR1946641     5  0.4666      0.468 0.000 0.420 0.044  0 0.536 0.000
#&gt; SRR1946656     1  0.3250      0.752 0.788 0.004 0.012  0 0.000 0.196
#&gt; SRR1946640     5  0.4666      0.468 0.000 0.420 0.044  0 0.536 0.000
#&gt; SRR1946639     5  0.4666      0.468 0.000 0.420 0.044  0 0.536 0.000
#&gt; SRR1946638     5  0.4666      0.468 0.000 0.420 0.044  0 0.536 0.000
#&gt; SRR1946637     5  0.4666      0.468 0.000 0.420 0.044  0 0.536 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.620           0.790       0.899         0.4935 0.495   0.495
#> 3 3 0.353           0.445       0.713         0.2955 0.644   0.404
#> 4 4 0.466           0.567       0.730         0.1384 0.737   0.396
#> 5 5 0.642           0.594       0.731         0.0786 0.833   0.496
#> 6 6 0.767           0.699       0.822         0.0512 0.909   0.628
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.9970     0.3225 0.468 0.532
#&gt; SRR1946691     2  0.0000     0.8554 0.000 1.000
#&gt; SRR1946690     2  0.0000     0.8554 0.000 1.000
#&gt; SRR1946689     2  0.2236     0.8500 0.036 0.964
#&gt; SRR1946686     1  0.0000     0.9206 1.000 0.000
#&gt; SRR1946685     2  0.7602     0.7395 0.220 0.780
#&gt; SRR1946688     2  0.0672     0.8569 0.008 0.992
#&gt; SRR1946684     1  0.2236     0.9223 0.964 0.036
#&gt; SRR1946683     1  0.2043     0.9233 0.968 0.032
#&gt; SRR1946682     2  0.7950     0.7048 0.240 0.760
#&gt; SRR1946680     2  0.2043     0.8511 0.032 0.968
#&gt; SRR1946681     2  0.0000     0.8554 0.000 1.000
#&gt; SRR1946687     2  1.0000     0.2351 0.496 0.504
#&gt; SRR1946679     2  0.7602     0.7395 0.220 0.780
#&gt; SRR1946678     1  0.0938     0.9234 0.988 0.012
#&gt; SRR1946676     2  0.7745     0.7310 0.228 0.772
#&gt; SRR1946677     1  0.2778     0.9193 0.952 0.048
#&gt; SRR1946672     2  0.9393     0.5678 0.356 0.644
#&gt; SRR1946673     1  0.4431     0.8803 0.908 0.092
#&gt; SRR1946671     1  0.2778     0.9193 0.952 0.048
#&gt; SRR1946669     1  0.2236     0.9223 0.964 0.036
#&gt; SRR1946668     1  0.2236     0.9223 0.964 0.036
#&gt; SRR1946666     1  0.0000     0.9206 1.000 0.000
#&gt; SRR1946667     2  0.2236     0.8500 0.036 0.964
#&gt; SRR1946670     2  0.0672     0.8569 0.008 0.992
#&gt; SRR1946663     1  0.9983    -0.0718 0.524 0.476
#&gt; SRR1946664     2  0.0000     0.8554 0.000 1.000
#&gt; SRR1946662     1  0.2236     0.9223 0.964 0.036
#&gt; SRR1946661     1  0.4431     0.8803 0.908 0.092
#&gt; SRR1946660     2  0.0672     0.8569 0.008 0.992
#&gt; SRR1946659     1  0.0000     0.9206 1.000 0.000
#&gt; SRR1946658     2  0.0672     0.8569 0.008 0.992
#&gt; SRR1946657     2  0.0938     0.8567 0.012 0.988
#&gt; SRR1946655     2  0.2236     0.8500 0.036 0.964
#&gt; SRR1946654     2  0.6531     0.8006 0.168 0.832
#&gt; SRR1946653     2  0.9286     0.5867 0.344 0.656
#&gt; SRR1946652     2  0.7602     0.7395 0.220 0.780
#&gt; SRR1946651     2  0.3733     0.8352 0.072 0.928
#&gt; SRR1946650     2  0.9775     0.3914 0.412 0.588
#&gt; SRR1946649     1  0.2778     0.9193 0.952 0.048
#&gt; SRR1946648     1  0.9970    -0.1787 0.532 0.468
#&gt; SRR1946647     1  0.2236     0.9235 0.964 0.036
#&gt; SRR1946646     2  0.2948     0.8532 0.052 0.948
#&gt; SRR1946645     1  0.2423     0.9223 0.960 0.040
#&gt; SRR1946644     2  0.0000     0.8554 0.000 1.000
#&gt; SRR1946643     2  0.2236     0.8500 0.036 0.964
#&gt; SRR1946642     1  0.0938     0.9234 0.988 0.012
#&gt; SRR1946641     1  0.0000     0.9206 1.000 0.000
#&gt; SRR1946656     2  0.2236     0.8500 0.036 0.964
#&gt; SRR1946640     1  0.0000     0.9206 1.000 0.000
#&gt; SRR1946639     1  0.0000     0.9206 1.000 0.000
#&gt; SRR1946638     1  0.0000     0.9206 1.000 0.000
#&gt; SRR1946637     1  0.0000     0.9206 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.9872     0.3469 0.272 0.320 0.408
#&gt; SRR1946691     3  0.5988     0.3131 0.000 0.368 0.632
#&gt; SRR1946690     3  0.6008     0.3134 0.000 0.372 0.628
#&gt; SRR1946689     3  0.1163     0.5904 0.000 0.028 0.972
#&gt; SRR1946686     1  0.3310     0.7517 0.908 0.064 0.028
#&gt; SRR1946685     2  0.0983     0.6000 0.004 0.980 0.016
#&gt; SRR1946688     2  0.6225     0.1496 0.000 0.568 0.432
#&gt; SRR1946684     1  0.6280     0.1912 0.540 0.460 0.000
#&gt; SRR1946683     2  0.6302    -0.1118 0.480 0.520 0.000
#&gt; SRR1946682     2  0.5061     0.5062 0.008 0.784 0.208
#&gt; SRR1946680     3  0.1163     0.5904 0.000 0.028 0.972
#&gt; SRR1946681     3  0.4750     0.5991 0.000 0.216 0.784
#&gt; SRR1946687     3  0.8837     0.2158 0.424 0.116 0.460
#&gt; SRR1946679     2  0.0237     0.6036 0.004 0.996 0.000
#&gt; SRR1946678     1  0.0592     0.7888 0.988 0.012 0.000
#&gt; SRR1946676     2  0.1163     0.5955 0.000 0.972 0.028
#&gt; SRR1946677     2  0.5733     0.3361 0.324 0.676 0.000
#&gt; SRR1946672     3  0.9680     0.4487 0.244 0.300 0.456
#&gt; SRR1946673     2  0.5098     0.4630 0.248 0.752 0.000
#&gt; SRR1946671     2  0.5835     0.3020 0.340 0.660 0.000
#&gt; SRR1946669     1  0.6154     0.3110 0.592 0.408 0.000
#&gt; SRR1946668     1  0.6308     0.1031 0.508 0.492 0.000
#&gt; SRR1946666     1  0.3649     0.7301 0.896 0.068 0.036
#&gt; SRR1946667     3  0.1163     0.5904 0.000 0.028 0.972
#&gt; SRR1946670     2  0.6225     0.1496 0.000 0.568 0.432
#&gt; SRR1946663     2  0.5987     0.5171 0.036 0.756 0.208
#&gt; SRR1946664     3  0.6045     0.2970 0.000 0.380 0.620
#&gt; SRR1946662     1  0.6280     0.1912 0.540 0.460 0.000
#&gt; SRR1946661     2  0.3482     0.5946 0.128 0.872 0.000
#&gt; SRR1946660     2  0.5988     0.2879 0.000 0.632 0.368
#&gt; SRR1946659     1  0.2689     0.7413 0.932 0.032 0.036
#&gt; SRR1946658     2  0.5760     0.3047 0.000 0.672 0.328
#&gt; SRR1946657     2  0.0000     0.6022 0.000 1.000 0.000
#&gt; SRR1946655     3  0.5493     0.6077 0.012 0.232 0.756
#&gt; SRR1946654     3  0.9355     0.4758 0.188 0.320 0.492
#&gt; SRR1946653     3  0.9624     0.4603 0.256 0.272 0.472
#&gt; SRR1946652     2  0.0661     0.6040 0.004 0.988 0.008
#&gt; SRR1946651     2  0.0592     0.6015 0.000 0.988 0.012
#&gt; SRR1946650     2  0.1399     0.6085 0.028 0.968 0.004
#&gt; SRR1946649     2  0.5497     0.3951 0.292 0.708 0.000
#&gt; SRR1946648     2  0.9386     0.0612 0.204 0.500 0.296
#&gt; SRR1946647     2  0.6307    -0.1435 0.488 0.512 0.000
#&gt; SRR1946646     2  0.6113     0.0859 0.012 0.688 0.300
#&gt; SRR1946645     2  0.6168     0.1559 0.412 0.588 0.000
#&gt; SRR1946644     2  0.6647    -0.2930 0.008 0.540 0.452
#&gt; SRR1946643     3  0.5450     0.6117 0.012 0.228 0.760
#&gt; SRR1946642     1  0.0592     0.7888 0.988 0.012 0.000
#&gt; SRR1946641     1  0.0592     0.7888 0.988 0.012 0.000
#&gt; SRR1946656     3  0.5450     0.6117 0.012 0.228 0.760
#&gt; SRR1946640     1  0.0592     0.7888 0.988 0.012 0.000
#&gt; SRR1946639     1  0.0592     0.7888 0.988 0.012 0.000
#&gt; SRR1946638     1  0.0592     0.7888 0.988 0.012 0.000
#&gt; SRR1946637     1  0.0592     0.7888 0.988 0.012 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3   0.587     0.6832 0.144 0.108 0.732 0.016
#&gt; SRR1946691     4   0.241     0.6729 0.000 0.044 0.036 0.920
#&gt; SRR1946690     4   0.403     0.6730 0.000 0.092 0.072 0.836
#&gt; SRR1946689     4   0.654     0.3356 0.064 0.004 0.432 0.500
#&gt; SRR1946686     1   0.703     0.0875 0.496 0.124 0.380 0.000
#&gt; SRR1946685     2   0.642     0.4963 0.000 0.632 0.120 0.248
#&gt; SRR1946688     4   0.302     0.6085 0.000 0.148 0.000 0.852
#&gt; SRR1946684     2   0.518     0.6056 0.196 0.740 0.000 0.064
#&gt; SRR1946683     2   0.388     0.6752 0.076 0.852 0.068 0.004
#&gt; SRR1946682     2   0.495     0.3149 0.000 0.560 0.000 0.440
#&gt; SRR1946680     4   0.654     0.3356 0.064 0.004 0.432 0.500
#&gt; SRR1946681     4   0.566     0.4797 0.000 0.032 0.368 0.600
#&gt; SRR1946687     3   0.583     0.6267 0.196 0.076 0.716 0.012
#&gt; SRR1946679     2   0.579     0.4761 0.000 0.640 0.052 0.308
#&gt; SRR1946678     1   0.201     0.8354 0.920 0.080 0.000 0.000
#&gt; SRR1946676     2   0.596     0.5604 0.000 0.688 0.116 0.196
#&gt; SRR1946677     2   0.351     0.6855 0.064 0.872 0.060 0.004
#&gt; SRR1946672     3   0.570     0.6957 0.124 0.092 0.756 0.028
#&gt; SRR1946673     2   0.301     0.7003 0.056 0.892 0.000 0.052
#&gt; SRR1946671     2   0.380     0.6805 0.064 0.860 0.068 0.008
#&gt; SRR1946669     2   0.496     0.4958 0.300 0.684 0.000 0.016
#&gt; SRR1946668     2   0.468     0.6288 0.176 0.776 0.000 0.048
#&gt; SRR1946666     3   0.699     0.0798 0.412 0.116 0.472 0.000
#&gt; SRR1946667     4   0.654     0.3356 0.064 0.004 0.432 0.500
#&gt; SRR1946670     4   0.307     0.6079 0.000 0.152 0.000 0.848
#&gt; SRR1946663     2   0.495     0.3149 0.000 0.560 0.000 0.440
#&gt; SRR1946664     4   0.409     0.6718 0.000 0.096 0.072 0.832
#&gt; SRR1946662     2   0.418     0.6428 0.180 0.796 0.000 0.024
#&gt; SRR1946661     2   0.381     0.6572 0.012 0.812 0.000 0.176
#&gt; SRR1946660     4   0.302     0.6085 0.000 0.148 0.000 0.852
#&gt; SRR1946659     1   0.611     0.0125 0.524 0.048 0.428 0.000
#&gt; SRR1946658     4   0.451     0.4827 0.000 0.224 0.020 0.756
#&gt; SRR1946657     2   0.622     0.4324 0.000 0.608 0.076 0.316
#&gt; SRR1946655     3   0.201     0.5868 0.000 0.000 0.920 0.080
#&gt; SRR1946654     3   0.555     0.6960 0.076 0.112 0.772 0.040
#&gt; SRR1946653     3   0.581     0.6871 0.144 0.096 0.740 0.020
#&gt; SRR1946652     2   0.502     0.5747 0.000 0.724 0.036 0.240
#&gt; SRR1946651     2   0.585     0.4588 0.000 0.628 0.052 0.320
#&gt; SRR1946650     2   0.414     0.6317 0.000 0.800 0.024 0.176
#&gt; SRR1946649     2   0.269     0.7031 0.036 0.916 0.036 0.012
#&gt; SRR1946648     3   0.600     0.5635 0.048 0.304 0.640 0.008
#&gt; SRR1946647     2   0.482     0.6342 0.160 0.784 0.008 0.048
#&gt; SRR1946646     3   0.781     0.0775 0.000 0.296 0.420 0.284
#&gt; SRR1946645     2   0.415     0.6632 0.084 0.836 0.076 0.004
#&gt; SRR1946644     4   0.662     0.4817 0.000 0.180 0.192 0.628
#&gt; SRR1946643     3   0.340     0.4980 0.004 0.000 0.832 0.164
#&gt; SRR1946642     1   0.201     0.8354 0.920 0.080 0.000 0.000
#&gt; SRR1946641     1   0.190     0.8477 0.932 0.064 0.004 0.000
#&gt; SRR1946656     3   0.340     0.4980 0.004 0.000 0.832 0.164
#&gt; SRR1946640     1   0.190     0.8477 0.932 0.064 0.004 0.000
#&gt; SRR1946639     1   0.190     0.8477 0.932 0.064 0.004 0.000
#&gt; SRR1946638     1   0.190     0.8477 0.932 0.064 0.004 0.000
#&gt; SRR1946637     1   0.190     0.8477 0.932 0.064 0.004 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3   0.202     0.7717 0.080 0.000 0.912 0.000 0.008
#&gt; SRR1946691     2   0.641     0.3408 0.036 0.560 0.012 0.332 0.060
#&gt; SRR1946690     2   0.454     0.4060 0.008 0.700 0.024 0.268 0.000
#&gt; SRR1946689     4   0.260     0.9911 0.000 0.004 0.120 0.872 0.004
#&gt; SRR1946686     3   0.466     0.6303 0.260 0.000 0.692 0.000 0.048
#&gt; SRR1946685     2   0.517     0.3481 0.000 0.648 0.076 0.000 0.276
#&gt; SRR1946688     2   0.665     0.3645 0.036 0.564 0.012 0.300 0.088
#&gt; SRR1946684     5   0.243     0.7118 0.040 0.028 0.000 0.020 0.912
#&gt; SRR1946683     5   0.526     0.6776 0.036 0.104 0.128 0.000 0.732
#&gt; SRR1946682     5   0.673     0.1950 0.036 0.280 0.000 0.140 0.544
#&gt; SRR1946680     4   0.249     0.9822 0.000 0.004 0.124 0.872 0.000
#&gt; SRR1946681     2   0.671    -0.0871 0.012 0.452 0.144 0.388 0.004
#&gt; SRR1946687     3   0.225     0.7702 0.088 0.000 0.900 0.000 0.012
#&gt; SRR1946679     2   0.476     0.3745 0.000 0.676 0.048 0.000 0.276
#&gt; SRR1946678     1   0.127     0.9658 0.948 0.000 0.000 0.000 0.052
#&gt; SRR1946676     2   0.607     0.0995 0.000 0.512 0.132 0.000 0.356
#&gt; SRR1946677     5   0.510     0.6867 0.032 0.112 0.112 0.000 0.744
#&gt; SRR1946672     3   0.191     0.7656 0.056 0.008 0.928 0.000 0.008
#&gt; SRR1946673     5   0.166     0.7314 0.024 0.016 0.008 0.004 0.948
#&gt; SRR1946671     5   0.516     0.6816 0.028 0.116 0.120 0.000 0.736
#&gt; SRR1946669     5   0.239     0.7163 0.104 0.000 0.004 0.004 0.888
#&gt; SRR1946668     5   0.283     0.7181 0.040 0.028 0.012 0.020 0.900
#&gt; SRR1946666     3   0.362     0.7255 0.192 0.000 0.788 0.000 0.020
#&gt; SRR1946667     4   0.260     0.9911 0.000 0.004 0.120 0.872 0.004
#&gt; SRR1946670     2   0.695     0.3592 0.036 0.548 0.016 0.288 0.112
#&gt; SRR1946663     5   0.673     0.1950 0.036 0.280 0.000 0.140 0.544
#&gt; SRR1946664     2   0.452     0.4082 0.008 0.704 0.024 0.264 0.000
#&gt; SRR1946662     5   0.207     0.7309 0.056 0.008 0.008 0.004 0.924
#&gt; SRR1946661     5   0.176     0.7096 0.008 0.064 0.000 0.000 0.928
#&gt; SRR1946660     2   0.665     0.3645 0.036 0.564 0.012 0.300 0.088
#&gt; SRR1946659     3   0.361     0.6609 0.268 0.000 0.732 0.000 0.000
#&gt; SRR1946658     2   0.646     0.4202 0.036 0.640 0.016 0.188 0.120
#&gt; SRR1946657     2   0.459     0.4070 0.004 0.716 0.044 0.000 0.236
#&gt; SRR1946655     3   0.393     0.5455 0.008 0.016 0.784 0.188 0.004
#&gt; SRR1946654     3   0.148     0.7276 0.000 0.048 0.944 0.000 0.008
#&gt; SRR1946653     3   0.189     0.7717 0.080 0.000 0.916 0.000 0.004
#&gt; SRR1946652     2   0.497     0.1122 0.000 0.564 0.032 0.000 0.404
#&gt; SRR1946651     2   0.467     0.3791 0.000 0.684 0.044 0.000 0.272
#&gt; SRR1946650     5   0.485     0.2721 0.000 0.424 0.024 0.000 0.552
#&gt; SRR1946649     5   0.532     0.6068 0.016 0.216 0.080 0.000 0.688
#&gt; SRR1946648     3   0.339     0.6748 0.008 0.020 0.832 0.000 0.140
#&gt; SRR1946647     5   0.295     0.7177 0.036 0.024 0.024 0.020 0.896
#&gt; SRR1946646     2   0.466     0.3854 0.000 0.668 0.296 0.000 0.036
#&gt; SRR1946645     5   0.535     0.6753 0.036 0.112 0.128 0.000 0.724
#&gt; SRR1946644     2   0.485     0.4335 0.004 0.756 0.144 0.080 0.016
#&gt; SRR1946643     3   0.559     0.2275 0.012 0.052 0.604 0.328 0.004
#&gt; SRR1946642     1   0.127     0.9658 0.948 0.000 0.000 0.000 0.052
#&gt; SRR1946641     1   0.149     0.9864 0.948 0.000 0.024 0.000 0.028
#&gt; SRR1946656     3   0.559     0.2275 0.012 0.052 0.604 0.328 0.004
#&gt; SRR1946640     1   0.149     0.9864 0.948 0.000 0.024 0.000 0.028
#&gt; SRR1946639     1   0.149     0.9864 0.948 0.000 0.024 0.000 0.028
#&gt; SRR1946638     1   0.149     0.9864 0.948 0.000 0.024 0.000 0.028
#&gt; SRR1946637     1   0.149     0.9864 0.948 0.000 0.024 0.000 0.028
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.1176     0.8198 0.024 0.020 0.956 0.000 0.000 0.000
#&gt; SRR1946691     6  0.1707     0.6573 0.004 0.056 0.000 0.012 0.000 0.928
#&gt; SRR1946690     6  0.5105     0.2609 0.004 0.444 0.008 0.048 0.000 0.496
#&gt; SRR1946689     4  0.2608     0.9656 0.000 0.000 0.048 0.872 0.000 0.080
#&gt; SRR1946686     3  0.3339     0.7493 0.120 0.008 0.824 0.000 0.048 0.000
#&gt; SRR1946685     2  0.2039     0.7841 0.000 0.908 0.016 0.000 0.072 0.004
#&gt; SRR1946688     6  0.1382     0.6611 0.000 0.036 0.000 0.008 0.008 0.948
#&gt; SRR1946684     5  0.1485     0.7240 0.028 0.000 0.000 0.004 0.944 0.024
#&gt; SRR1946683     5  0.6005     0.6286 0.008 0.268 0.056 0.064 0.596 0.008
#&gt; SRR1946682     6  0.4004     0.4526 0.000 0.004 0.000 0.012 0.328 0.656
#&gt; SRR1946680     4  0.3323     0.9315 0.004 0.008 0.056 0.844 0.004 0.084
#&gt; SRR1946681     6  0.7535     0.0873 0.008 0.300 0.088 0.192 0.012 0.400
#&gt; SRR1946687     3  0.1257     0.8194 0.028 0.020 0.952 0.000 0.000 0.000
#&gt; SRR1946679     2  0.2294     0.7877 0.000 0.892 0.000 0.000 0.072 0.036
#&gt; SRR1946678     1  0.0363     0.9808 0.988 0.000 0.000 0.000 0.012 0.000
#&gt; SRR1946676     2  0.4276     0.6605 0.000 0.752 0.020 0.048 0.176 0.004
#&gt; SRR1946677     5  0.5969     0.6288 0.008 0.272 0.052 0.064 0.596 0.008
#&gt; SRR1946672     3  0.0363     0.8135 0.000 0.012 0.988 0.000 0.000 0.000
#&gt; SRR1946673     5  0.1464     0.7385 0.016 0.036 0.000 0.000 0.944 0.004
#&gt; SRR1946671     5  0.5856     0.6315 0.008 0.272 0.044 0.064 0.604 0.008
#&gt; SRR1946669     5  0.1297     0.7360 0.040 0.012 0.000 0.000 0.948 0.000
#&gt; SRR1946668     5  0.1401     0.7263 0.028 0.000 0.000 0.004 0.948 0.020
#&gt; SRR1946666     3  0.2225     0.7942 0.092 0.008 0.892 0.000 0.008 0.000
#&gt; SRR1946667     4  0.2608     0.9656 0.000 0.000 0.048 0.872 0.000 0.080
#&gt; SRR1946670     6  0.1821     0.6605 0.000 0.040 0.000 0.008 0.024 0.928
#&gt; SRR1946663     6  0.4004     0.4526 0.000 0.004 0.000 0.012 0.328 0.656
#&gt; SRR1946664     6  0.5105     0.2609 0.004 0.444 0.008 0.048 0.000 0.496
#&gt; SRR1946662     5  0.1168     0.7385 0.028 0.016 0.000 0.000 0.956 0.000
#&gt; SRR1946661     5  0.4490     0.6934 0.000 0.172 0.000 0.064 0.736 0.028
#&gt; SRR1946660     6  0.1382     0.6611 0.000 0.036 0.000 0.008 0.008 0.948
#&gt; SRR1946659     3  0.2178     0.7749 0.132 0.000 0.868 0.000 0.000 0.000
#&gt; SRR1946658     6  0.2526     0.6567 0.000 0.096 0.000 0.004 0.024 0.876
#&gt; SRR1946657     2  0.2295     0.7324 0.000 0.908 0.004 0.024 0.016 0.048
#&gt; SRR1946655     3  0.3776     0.6975 0.008 0.032 0.832 0.080 0.012 0.036
#&gt; SRR1946654     3  0.0547     0.8124 0.000 0.020 0.980 0.000 0.000 0.000
#&gt; SRR1946653     3  0.1088     0.8199 0.024 0.016 0.960 0.000 0.000 0.000
#&gt; SRR1946652     2  0.3849     0.6485 0.000 0.752 0.000 0.032 0.208 0.008
#&gt; SRR1946651     2  0.2784     0.7808 0.000 0.876 0.000 0.020 0.064 0.040
#&gt; SRR1946650     2  0.4769     0.4609 0.000 0.652 0.000 0.068 0.272 0.008
#&gt; SRR1946649     5  0.5417     0.5318 0.008 0.344 0.004 0.068 0.568 0.008
#&gt; SRR1946648     3  0.2798     0.7673 0.000 0.048 0.876 0.020 0.056 0.000
#&gt; SRR1946647     5  0.1743     0.7189 0.028 0.000 0.008 0.004 0.936 0.024
#&gt; SRR1946646     2  0.2844     0.6919 0.000 0.864 0.092 0.004 0.004 0.036
#&gt; SRR1946645     5  0.6074     0.6212 0.008 0.272 0.060 0.064 0.588 0.008
#&gt; SRR1946644     2  0.4203     0.5305 0.004 0.772 0.040 0.036 0.000 0.148
#&gt; SRR1946643     3  0.6622     0.1810 0.008 0.116 0.508 0.312 0.012 0.044
#&gt; SRR1946642     1  0.0363     0.9808 0.988 0.000 0.000 0.000 0.012 0.000
#&gt; SRR1946641     1  0.0717     0.9924 0.976 0.000 0.016 0.000 0.008 0.000
#&gt; SRR1946656     3  0.6622     0.1810 0.008 0.116 0.508 0.312 0.012 0.044
#&gt; SRR1946640     1  0.0717     0.9924 0.976 0.000 0.016 0.000 0.008 0.000
#&gt; SRR1946639     1  0.0717     0.9924 0.976 0.000 0.016 0.000 0.008 0.000
#&gt; SRR1946638     1  0.0717     0.9924 0.976 0.000 0.016 0.000 0.008 0.000
#&gt; SRR1946637     1  0.0717     0.9924 0.976 0.000 0.016 0.000 0.008 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.847           0.891       0.958         0.5093 0.491   0.491
#> 3 3 0.602           0.783       0.874         0.3229 0.720   0.490
#> 4 4 0.666           0.721       0.801         0.1256 0.800   0.477
#> 5 5 0.681           0.592       0.788         0.0654 0.896   0.608
#> 6 6 0.719           0.558       0.700         0.0405 0.898   0.547
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2   0.961     0.3836 0.384 0.616
#&gt; SRR1946691     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946690     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946689     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946686     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946685     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946688     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946684     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946683     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946682     1   0.958     0.3762 0.620 0.380
#&gt; SRR1946680     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946681     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946687     1   0.388     0.8827 0.924 0.076
#&gt; SRR1946679     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946678     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946676     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946677     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946672     2   0.738     0.7278 0.208 0.792
#&gt; SRR1946673     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946671     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946669     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946668     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946666     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946667     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946670     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946663     1   0.518     0.8374 0.884 0.116
#&gt; SRR1946664     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946662     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946661     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946660     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946659     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946658     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946657     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946655     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946654     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946653     2   0.745     0.7221 0.212 0.788
#&gt; SRR1946652     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946651     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946650     2   0.949     0.3881 0.368 0.632
#&gt; SRR1946649     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946648     1   0.998     0.0291 0.528 0.472
#&gt; SRR1946647     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946646     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946645     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946644     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946643     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946642     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946641     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946656     2   0.000     0.9512 0.000 1.000
#&gt; SRR1946640     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946639     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946638     1   0.000     0.9546 1.000 0.000
#&gt; SRR1946637     1   0.000     0.9546 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.0424      0.819 0.008 0.000 0.992
#&gt; SRR1946691     2  0.1031      0.857 0.000 0.976 0.024
#&gt; SRR1946690     2  0.1163      0.855 0.000 0.972 0.028
#&gt; SRR1946689     3  0.5431      0.718 0.000 0.284 0.716
#&gt; SRR1946686     1  0.6079      0.593 0.612 0.000 0.388
#&gt; SRR1946685     2  0.2056      0.859 0.024 0.952 0.024
#&gt; SRR1946688     2  0.1129      0.861 0.004 0.976 0.020
#&gt; SRR1946684     1  0.0424      0.864 0.992 0.008 0.000
#&gt; SRR1946683     1  0.1647      0.871 0.960 0.004 0.036
#&gt; SRR1946682     2  0.4178      0.785 0.172 0.828 0.000
#&gt; SRR1946680     3  0.5431      0.718 0.000 0.284 0.716
#&gt; SRR1946681     2  0.3116      0.790 0.000 0.892 0.108
#&gt; SRR1946687     3  0.1289      0.800 0.032 0.000 0.968
#&gt; SRR1946679     2  0.1711      0.859 0.032 0.960 0.008
#&gt; SRR1946678     1  0.3752      0.863 0.856 0.000 0.144
#&gt; SRR1946676     2  0.5028      0.767 0.040 0.828 0.132
#&gt; SRR1946677     1  0.1031      0.857 0.976 0.024 0.000
#&gt; SRR1946672     3  0.0424      0.819 0.008 0.000 0.992
#&gt; SRR1946673     1  0.4555      0.648 0.800 0.200 0.000
#&gt; SRR1946671     1  0.1636      0.866 0.964 0.020 0.016
#&gt; SRR1946669     1  0.0424      0.864 0.992 0.008 0.000
#&gt; SRR1946668     1  0.0237      0.866 0.996 0.004 0.000
#&gt; SRR1946666     1  0.6244      0.492 0.560 0.000 0.440
#&gt; SRR1946667     3  0.5431      0.718 0.000 0.284 0.716
#&gt; SRR1946670     2  0.1129      0.861 0.004 0.976 0.020
#&gt; SRR1946663     2  0.4504      0.770 0.196 0.804 0.000
#&gt; SRR1946664     2  0.1031      0.857 0.000 0.976 0.024
#&gt; SRR1946662     1  0.0592      0.863 0.988 0.012 0.000
#&gt; SRR1946661     2  0.5988      0.518 0.368 0.632 0.000
#&gt; SRR1946660     2  0.0661      0.862 0.004 0.988 0.008
#&gt; SRR1946659     3  0.2537      0.749 0.080 0.000 0.920
#&gt; SRR1946658     2  0.1129      0.861 0.004 0.976 0.020
#&gt; SRR1946657     2  0.1015      0.862 0.008 0.980 0.012
#&gt; SRR1946655     3  0.4121      0.799 0.000 0.168 0.832
#&gt; SRR1946654     3  0.0892      0.825 0.000 0.020 0.980
#&gt; SRR1946653     3  0.0424      0.819 0.008 0.000 0.992
#&gt; SRR1946652     2  0.4228      0.801 0.148 0.844 0.008
#&gt; SRR1946651     2  0.1163      0.860 0.028 0.972 0.000
#&gt; SRR1946650     2  0.4399      0.773 0.188 0.812 0.000
#&gt; SRR1946649     1  0.1163      0.855 0.972 0.028 0.000
#&gt; SRR1946648     3  0.1163      0.817 0.028 0.000 0.972
#&gt; SRR1946647     1  0.1267      0.870 0.972 0.004 0.024
#&gt; SRR1946646     3  0.6274      0.348 0.000 0.456 0.544
#&gt; SRR1946645     1  0.4345      0.865 0.848 0.016 0.136
#&gt; SRR1946644     2  0.6244     -0.106 0.000 0.560 0.440
#&gt; SRR1946643     3  0.4121      0.799 0.000 0.168 0.832
#&gt; SRR1946642     1  0.3752      0.863 0.856 0.000 0.144
#&gt; SRR1946641     1  0.4121      0.855 0.832 0.000 0.168
#&gt; SRR1946656     3  0.4121      0.799 0.000 0.168 0.832
#&gt; SRR1946640     1  0.4121      0.855 0.832 0.000 0.168
#&gt; SRR1946639     1  0.4121      0.855 0.832 0.000 0.168
#&gt; SRR1946638     1  0.4121      0.855 0.832 0.000 0.168
#&gt; SRR1946637     1  0.4121      0.855 0.832 0.000 0.168
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.1557      0.843 0.056 0.000 0.944 0.000
#&gt; SRR1946691     4  0.0188      0.848 0.000 0.004 0.000 0.996
#&gt; SRR1946690     4  0.2036      0.836 0.000 0.032 0.032 0.936
#&gt; SRR1946689     4  0.4193      0.724 0.000 0.000 0.268 0.732
#&gt; SRR1946686     1  0.4543      0.341 0.676 0.000 0.324 0.000
#&gt; SRR1946685     2  0.4307      0.758 0.000 0.808 0.048 0.144
#&gt; SRR1946688     4  0.0188      0.847 0.000 0.004 0.000 0.996
#&gt; SRR1946684     1  0.4655      0.735 0.760 0.208 0.000 0.032
#&gt; SRR1946683     1  0.3257      0.766 0.844 0.152 0.004 0.000
#&gt; SRR1946682     4  0.3806      0.749 0.020 0.156 0.000 0.824
#&gt; SRR1946680     4  0.4222      0.720 0.000 0.000 0.272 0.728
#&gt; SRR1946681     4  0.3895      0.790 0.000 0.012 0.184 0.804
#&gt; SRR1946687     3  0.1792      0.840 0.068 0.000 0.932 0.000
#&gt; SRR1946679     2  0.3946      0.760 0.000 0.812 0.020 0.168
#&gt; SRR1946678     1  0.0779      0.814 0.980 0.016 0.004 0.000
#&gt; SRR1946676     2  0.4374      0.759 0.000 0.812 0.068 0.120
#&gt; SRR1946677     2  0.4382      0.516 0.296 0.704 0.000 0.000
#&gt; SRR1946672     3  0.0921      0.843 0.028 0.000 0.972 0.000
#&gt; SRR1946673     2  0.4245      0.605 0.196 0.784 0.000 0.020
#&gt; SRR1946671     2  0.4477      0.510 0.312 0.688 0.000 0.000
#&gt; SRR1946669     1  0.3649      0.753 0.796 0.204 0.000 0.000
#&gt; SRR1946668     1  0.4466      0.754 0.784 0.180 0.000 0.036
#&gt; SRR1946666     3  0.4866      0.414 0.404 0.000 0.596 0.000
#&gt; SRR1946667     4  0.4193      0.724 0.000 0.000 0.268 0.732
#&gt; SRR1946670     4  0.0817      0.843 0.000 0.024 0.000 0.976
#&gt; SRR1946663     4  0.3806      0.749 0.020 0.156 0.000 0.824
#&gt; SRR1946664     4  0.1929      0.835 0.000 0.036 0.024 0.940
#&gt; SRR1946662     1  0.4250      0.689 0.724 0.276 0.000 0.000
#&gt; SRR1946661     2  0.4656      0.628 0.160 0.784 0.000 0.056
#&gt; SRR1946660     4  0.0188      0.847 0.000 0.004 0.000 0.996
#&gt; SRR1946659     3  0.4564      0.563 0.328 0.000 0.672 0.000
#&gt; SRR1946658     4  0.0469      0.846 0.000 0.012 0.000 0.988
#&gt; SRR1946657     2  0.4467      0.745 0.000 0.788 0.040 0.172
#&gt; SRR1946655     3  0.0779      0.830 0.000 0.004 0.980 0.016
#&gt; SRR1946654     3  0.0188      0.837 0.000 0.004 0.996 0.000
#&gt; SRR1946653     3  0.1557      0.843 0.056 0.000 0.944 0.000
#&gt; SRR1946652     2  0.2921      0.774 0.000 0.860 0.000 0.140
#&gt; SRR1946651     2  0.3925      0.757 0.000 0.808 0.016 0.176
#&gt; SRR1946650     2  0.2401      0.771 0.004 0.904 0.000 0.092
#&gt; SRR1946649     2  0.3649      0.649 0.204 0.796 0.000 0.000
#&gt; SRR1946648     3  0.2830      0.826 0.060 0.040 0.900 0.000
#&gt; SRR1946647     1  0.4423      0.756 0.788 0.176 0.000 0.036
#&gt; SRR1946646     3  0.7434      0.223 0.000 0.232 0.512 0.256
#&gt; SRR1946645     1  0.5168     -0.219 0.500 0.496 0.004 0.000
#&gt; SRR1946644     4  0.6284      0.640 0.000 0.164 0.172 0.664
#&gt; SRR1946643     3  0.1305      0.819 0.000 0.004 0.960 0.036
#&gt; SRR1946642     1  0.0779      0.814 0.980 0.016 0.004 0.000
#&gt; SRR1946641     1  0.0707      0.814 0.980 0.000 0.020 0.000
#&gt; SRR1946656     3  0.1209      0.822 0.000 0.004 0.964 0.032
#&gt; SRR1946640     1  0.0707      0.814 0.980 0.000 0.020 0.000
#&gt; SRR1946639     1  0.0707      0.814 0.980 0.000 0.020 0.000
#&gt; SRR1946638     1  0.0707      0.814 0.980 0.000 0.020 0.000
#&gt; SRR1946637     1  0.0707      0.814 0.980 0.000 0.020 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.1399     0.7946 0.028 0.000 0.952 0.000 0.020
#&gt; SRR1946691     4  0.1809     0.7740 0.000 0.012 0.000 0.928 0.060
#&gt; SRR1946690     4  0.2389     0.7133 0.000 0.116 0.000 0.880 0.004
#&gt; SRR1946689     4  0.3521     0.7104 0.000 0.008 0.172 0.808 0.012
#&gt; SRR1946686     1  0.4114     0.4292 0.712 0.000 0.272 0.000 0.016
#&gt; SRR1946685     2  0.1331     0.7047 0.000 0.952 0.000 0.040 0.008
#&gt; SRR1946688     4  0.2361     0.7720 0.000 0.012 0.000 0.892 0.096
#&gt; SRR1946684     5  0.4269     0.6002 0.300 0.000 0.000 0.016 0.684
#&gt; SRR1946683     1  0.5838     0.0740 0.552 0.112 0.000 0.000 0.336
#&gt; SRR1946682     4  0.4331     0.4875 0.000 0.004 0.000 0.596 0.400
#&gt; SRR1946680     4  0.3873     0.6726 0.000 0.008 0.212 0.768 0.012
#&gt; SRR1946681     4  0.5309     0.5778 0.000 0.080 0.228 0.680 0.012
#&gt; SRR1946687     3  0.3146     0.7374 0.128 0.000 0.844 0.000 0.028
#&gt; SRR1946679     2  0.1809     0.7027 0.000 0.928 0.000 0.060 0.012
#&gt; SRR1946678     1  0.0609     0.7759 0.980 0.000 0.000 0.000 0.020
#&gt; SRR1946676     2  0.3328     0.6167 0.000 0.812 0.008 0.004 0.176
#&gt; SRR1946677     5  0.6120     0.2734 0.140 0.300 0.000 0.004 0.556
#&gt; SRR1946672     3  0.0613     0.7951 0.004 0.008 0.984 0.000 0.004
#&gt; SRR1946673     5  0.3536     0.5437 0.032 0.156 0.000 0.000 0.812
#&gt; SRR1946671     5  0.6619     0.1994 0.212 0.304 0.000 0.004 0.480
#&gt; SRR1946669     5  0.4088     0.5591 0.368 0.000 0.000 0.000 0.632
#&gt; SRR1946668     5  0.4511     0.5621 0.356 0.000 0.000 0.016 0.628
#&gt; SRR1946666     3  0.4827     0.1743 0.476 0.000 0.504 0.000 0.020
#&gt; SRR1946667     4  0.3521     0.7104 0.000 0.008 0.172 0.808 0.012
#&gt; SRR1946670     4  0.2411     0.7718 0.000 0.008 0.000 0.884 0.108
#&gt; SRR1946663     4  0.4341     0.4802 0.000 0.004 0.000 0.592 0.404
#&gt; SRR1946664     4  0.2719     0.6920 0.000 0.144 0.000 0.852 0.004
#&gt; SRR1946662     5  0.4822     0.6156 0.288 0.048 0.000 0.000 0.664
#&gt; SRR1946661     5  0.3488     0.4773 0.000 0.168 0.000 0.024 0.808
#&gt; SRR1946660     4  0.2361     0.7720 0.000 0.012 0.000 0.892 0.096
#&gt; SRR1946659     3  0.4829     0.1713 0.480 0.000 0.500 0.000 0.020
#&gt; SRR1946658     4  0.3112     0.7616 0.000 0.044 0.000 0.856 0.100
#&gt; SRR1946657     2  0.2170     0.6933 0.000 0.904 0.004 0.088 0.004
#&gt; SRR1946655     3  0.0486     0.7928 0.000 0.004 0.988 0.004 0.004
#&gt; SRR1946654     3  0.0324     0.7936 0.000 0.004 0.992 0.000 0.004
#&gt; SRR1946653     3  0.1041     0.7966 0.032 0.000 0.964 0.000 0.004
#&gt; SRR1946652     2  0.2358     0.6635 0.000 0.888 0.000 0.008 0.104
#&gt; SRR1946651     2  0.2193     0.7040 0.000 0.912 0.000 0.060 0.028
#&gt; SRR1946650     2  0.3550     0.5602 0.000 0.760 0.000 0.004 0.236
#&gt; SRR1946649     2  0.6473     0.0243 0.164 0.468 0.000 0.004 0.364
#&gt; SRR1946648     3  0.2786     0.7615 0.020 0.012 0.884 0.000 0.084
#&gt; SRR1946647     5  0.4380     0.5923 0.292 0.000 0.004 0.016 0.688
#&gt; SRR1946646     2  0.6551     0.3575 0.000 0.552 0.196 0.236 0.016
#&gt; SRR1946645     1  0.6716    -0.1247 0.420 0.208 0.000 0.004 0.368
#&gt; SRR1946644     2  0.6116     0.0846 0.000 0.480 0.080 0.424 0.016
#&gt; SRR1946643     3  0.4341     0.6041 0.000 0.048 0.764 0.180 0.008
#&gt; SRR1946642     1  0.0510     0.7797 0.984 0.000 0.000 0.000 0.016
#&gt; SRR1946641     1  0.0000     0.7900 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.4160     0.6255 0.000 0.044 0.780 0.168 0.008
#&gt; SRR1946640     1  0.0000     0.7900 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.7900 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.7900 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.7900 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.4716     0.6381 0.032 0.004 0.600 0.008 0.356 0.000
#&gt; SRR1946691     6  0.3103     0.6629 0.000 0.048 0.080 0.004 0.012 0.856
#&gt; SRR1946690     6  0.6090     0.4689 0.000 0.188 0.264 0.004 0.016 0.528
#&gt; SRR1946689     6  0.5377     0.3353 0.000 0.040 0.460 0.004 0.028 0.468
#&gt; SRR1946686     1  0.4810     0.5223 0.624 0.000 0.084 0.000 0.292 0.000
#&gt; SRR1946685     2  0.2056     0.6766 0.000 0.904 0.012 0.080 0.000 0.004
#&gt; SRR1946688     6  0.0508     0.6821 0.000 0.004 0.000 0.000 0.012 0.984
#&gt; SRR1946684     5  0.5712     0.8937 0.100 0.000 0.000 0.284 0.580 0.036
#&gt; SRR1946683     4  0.4919     0.4779 0.348 0.016 0.000 0.592 0.044 0.000
#&gt; SRR1946682     6  0.4025     0.4569 0.000 0.000 0.000 0.048 0.232 0.720
#&gt; SRR1946680     3  0.5350    -0.3555 0.000 0.040 0.512 0.004 0.028 0.416
#&gt; SRR1946681     3  0.5417    -0.1252 0.000 0.148 0.584 0.000 0.004 0.264
#&gt; SRR1946687     3  0.6017     0.4274 0.180 0.008 0.428 0.000 0.384 0.000
#&gt; SRR1946679     2  0.2220     0.6830 0.000 0.908 0.000 0.044 0.012 0.036
#&gt; SRR1946678     1  0.0622     0.7887 0.980 0.000 0.000 0.008 0.012 0.000
#&gt; SRR1946676     2  0.3843     0.0723 0.000 0.548 0.000 0.452 0.000 0.000
#&gt; SRR1946677     4  0.2642     0.6238 0.064 0.032 0.000 0.884 0.020 0.000
#&gt; SRR1946672     3  0.4058     0.6576 0.016 0.004 0.660 0.000 0.320 0.000
#&gt; SRR1946673     5  0.4878     0.7805 0.012 0.024 0.000 0.400 0.556 0.008
#&gt; SRR1946671     4  0.3778     0.6679 0.128 0.048 0.000 0.800 0.024 0.000
#&gt; SRR1946669     5  0.5495     0.8500 0.164 0.000 0.000 0.288 0.548 0.000
#&gt; SRR1946668     5  0.5764     0.8816 0.140 0.000 0.000 0.260 0.576 0.024
#&gt; SRR1946666     1  0.5808     0.2510 0.472 0.004 0.164 0.000 0.360 0.000
#&gt; SRR1946667     6  0.5377     0.3353 0.000 0.040 0.460 0.004 0.028 0.468
#&gt; SRR1946670     6  0.1476     0.6795 0.000 0.008 0.004 0.012 0.028 0.948
#&gt; SRR1946663     6  0.4237     0.4341 0.000 0.004 0.000 0.048 0.244 0.704
#&gt; SRR1946664     6  0.6244     0.4098 0.000 0.256 0.224 0.004 0.016 0.500
#&gt; SRR1946662     5  0.5421     0.8793 0.092 0.008 0.000 0.336 0.560 0.004
#&gt; SRR1946661     4  0.4865    -0.1412 0.000 0.028 0.000 0.660 0.264 0.048
#&gt; SRR1946660     6  0.0767     0.6812 0.000 0.008 0.000 0.004 0.012 0.976
#&gt; SRR1946659     1  0.5329     0.4268 0.564 0.004 0.112 0.000 0.320 0.000
#&gt; SRR1946658     6  0.2392     0.6651 0.000 0.064 0.016 0.008 0.012 0.900
#&gt; SRR1946657     2  0.2189     0.6817 0.000 0.916 0.028 0.028 0.004 0.024
#&gt; SRR1946655     3  0.2996     0.6628 0.000 0.000 0.772 0.000 0.228 0.000
#&gt; SRR1946654     3  0.3468     0.6690 0.000 0.000 0.712 0.004 0.284 0.000
#&gt; SRR1946653     3  0.4570     0.6431 0.032 0.008 0.608 0.000 0.352 0.000
#&gt; SRR1946652     2  0.4078     0.4570 0.000 0.700 0.000 0.268 0.008 0.024
#&gt; SRR1946651     2  0.2265     0.6756 0.000 0.896 0.000 0.076 0.004 0.024
#&gt; SRR1946650     4  0.4118     0.2047 0.000 0.396 0.000 0.592 0.004 0.008
#&gt; SRR1946649     4  0.4299     0.5782 0.092 0.188 0.000 0.720 0.000 0.000
#&gt; SRR1946648     3  0.5881     0.6020 0.016 0.008 0.528 0.112 0.336 0.000
#&gt; SRR1946647     5  0.5722     0.8752 0.092 0.000 0.000 0.264 0.596 0.048
#&gt; SRR1946646     2  0.4905     0.5007 0.000 0.652 0.280 0.012 0.012 0.044
#&gt; SRR1946645     4  0.3807     0.6368 0.228 0.028 0.000 0.740 0.004 0.000
#&gt; SRR1946644     2  0.6053     0.2541 0.000 0.544 0.260 0.004 0.020 0.172
#&gt; SRR1946643     3  0.2250     0.4342 0.000 0.064 0.896 0.000 0.000 0.040
#&gt; SRR1946642     1  0.0622     0.7887 0.980 0.000 0.000 0.008 0.012 0.000
#&gt; SRR1946641     1  0.0000     0.8040 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.2058     0.4786 0.000 0.048 0.916 0.000 0.012 0.024
#&gt; SRR1946640     1  0.0000     0.8040 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.8040 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.8040 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.8040 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.569           0.861       0.933          0.404 0.623   0.623
#> 3 3 0.571           0.780       0.859          0.534 0.736   0.576
#> 4 4 0.689           0.822       0.919          0.113 0.811   0.555
#> 5 5 0.739           0.715       0.872          0.117 0.877   0.621
#> 6 6 0.776           0.701       0.879          0.054 0.910   0.643
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.7056      0.797 0.192 0.808
#&gt; SRR1946691     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946690     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946689     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946686     2  0.7139      0.793 0.196 0.804
#&gt; SRR1946685     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946688     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946684     1  0.2043      0.900 0.968 0.032
#&gt; SRR1946683     2  0.7056      0.799 0.192 0.808
#&gt; SRR1946682     2  0.0376      0.917 0.004 0.996
#&gt; SRR1946680     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946681     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946687     2  0.7139      0.793 0.196 0.804
#&gt; SRR1946679     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946678     1  0.0000      0.919 1.000 0.000
#&gt; SRR1946676     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946677     2  0.7376      0.715 0.208 0.792
#&gt; SRR1946672     2  0.6887      0.804 0.184 0.816
#&gt; SRR1946673     2  0.1843      0.903 0.028 0.972
#&gt; SRR1946671     2  0.0672      0.915 0.008 0.992
#&gt; SRR1946669     1  0.0000      0.919 1.000 0.000
#&gt; SRR1946668     2  0.8144      0.736 0.252 0.748
#&gt; SRR1946666     2  0.7139      0.793 0.196 0.804
#&gt; SRR1946667     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946670     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946663     2  0.5519      0.818 0.128 0.872
#&gt; SRR1946664     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946662     1  0.7056      0.750 0.808 0.192
#&gt; SRR1946661     2  0.6801      0.756 0.180 0.820
#&gt; SRR1946660     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946659     1  0.0376      0.917 0.996 0.004
#&gt; SRR1946658     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946657     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946655     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946654     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946653     2  0.7139      0.793 0.196 0.804
#&gt; SRR1946652     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946651     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946650     2  0.7139      0.734 0.196 0.804
#&gt; SRR1946649     1  0.7139      0.745 0.804 0.196
#&gt; SRR1946648     2  0.6973      0.801 0.188 0.812
#&gt; SRR1946647     2  0.7139      0.794 0.196 0.804
#&gt; SRR1946646     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946645     1  0.9710      0.162 0.600 0.400
#&gt; SRR1946644     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946643     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946642     1  0.0000      0.919 1.000 0.000
#&gt; SRR1946641     1  0.0000      0.919 1.000 0.000
#&gt; SRR1946656     2  0.0000      0.919 0.000 1.000
#&gt; SRR1946640     1  0.0000      0.919 1.000 0.000
#&gt; SRR1946639     1  0.0000      0.919 1.000 0.000
#&gt; SRR1946638     1  0.0000      0.919 1.000 0.000
#&gt; SRR1946637     1  0.0000      0.919 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3   0.254      0.818 0.080 0.000 0.920
#&gt; SRR1946691     2   0.400      0.875 0.000 0.840 0.160
#&gt; SRR1946690     2   0.400      0.875 0.000 0.840 0.160
#&gt; SRR1946689     2   0.455      0.634 0.000 0.800 0.200
#&gt; SRR1946686     3   0.254      0.818 0.080 0.000 0.920
#&gt; SRR1946685     3   0.382      0.746 0.000 0.148 0.852
#&gt; SRR1946688     2   0.400      0.875 0.000 0.840 0.160
#&gt; SRR1946684     1   0.171      0.882 0.960 0.032 0.008
#&gt; SRR1946683     3   0.245      0.819 0.076 0.000 0.924
#&gt; SRR1946682     2   0.400      0.875 0.000 0.840 0.160
#&gt; SRR1946680     3   0.412      0.715 0.000 0.168 0.832
#&gt; SRR1946681     3   0.440      0.712 0.000 0.188 0.812
#&gt; SRR1946687     3   0.254      0.818 0.080 0.000 0.920
#&gt; SRR1946679     3   0.497      0.660 0.000 0.236 0.764
#&gt; SRR1946678     1   0.000      0.910 1.000 0.000 0.000
#&gt; SRR1946676     3   0.296      0.779 0.000 0.100 0.900
#&gt; SRR1946677     3   0.773      0.574 0.192 0.132 0.676
#&gt; SRR1946672     3   0.236      0.820 0.072 0.000 0.928
#&gt; SRR1946673     3   0.640      0.629 0.040 0.236 0.724
#&gt; SRR1946671     3   0.359      0.792 0.028 0.076 0.896
#&gt; SRR1946669     1   0.000      0.910 1.000 0.000 0.000
#&gt; SRR1946668     3   0.514      0.702 0.252 0.000 0.748
#&gt; SRR1946666     3   0.254      0.818 0.080 0.000 0.920
#&gt; SRR1946667     2   0.497      0.589 0.000 0.764 0.236
#&gt; SRR1946670     2   0.611      0.652 0.000 0.604 0.396
#&gt; SRR1946663     2   0.656      0.794 0.040 0.708 0.252
#&gt; SRR1946664     2   0.400      0.875 0.000 0.840 0.160
#&gt; SRR1946662     1   0.541      0.726 0.820 0.104 0.076
#&gt; SRR1946661     2   0.502      0.799 0.000 0.760 0.240
#&gt; SRR1946660     2   0.400      0.875 0.000 0.840 0.160
#&gt; SRR1946659     1   0.000      0.910 1.000 0.000 0.000
#&gt; SRR1946658     2   0.400      0.875 0.000 0.840 0.160
#&gt; SRR1946657     3   0.497      0.660 0.000 0.236 0.764
#&gt; SRR1946655     3   0.000      0.819 0.000 0.000 1.000
#&gt; SRR1946654     3   0.000      0.819 0.000 0.000 1.000
#&gt; SRR1946653     3   0.254      0.818 0.080 0.000 0.920
#&gt; SRR1946652     3   0.518      0.634 0.000 0.256 0.744
#&gt; SRR1946651     2   0.406      0.872 0.000 0.836 0.164
#&gt; SRR1946650     2   0.556      0.701 0.000 0.700 0.300
#&gt; SRR1946649     1   0.611      0.673 0.780 0.140 0.080
#&gt; SRR1946648     3   0.245      0.819 0.076 0.000 0.924
#&gt; SRR1946647     3   0.254      0.818 0.080 0.000 0.920
#&gt; SRR1946646     3   0.000      0.819 0.000 0.000 1.000
#&gt; SRR1946645     1   0.613      0.145 0.600 0.000 0.400
#&gt; SRR1946644     3   0.583      0.467 0.000 0.340 0.660
#&gt; SRR1946643     3   0.000      0.819 0.000 0.000 1.000
#&gt; SRR1946642     1   0.000      0.910 1.000 0.000 0.000
#&gt; SRR1946641     1   0.000      0.910 1.000 0.000 0.000
#&gt; SRR1946656     3   0.000      0.819 0.000 0.000 1.000
#&gt; SRR1946640     1   0.000      0.910 1.000 0.000 0.000
#&gt; SRR1946639     1   0.000      0.910 1.000 0.000 0.000
#&gt; SRR1946638     1   0.000      0.910 1.000 0.000 0.000
#&gt; SRR1946637     1   0.000      0.910 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1946675     3  0.0000      0.868 0.000 0.000 1.000  0
#&gt; SRR1946691     2  0.0336      0.904 0.000 0.992 0.008  0
#&gt; SRR1946690     2  0.0000      0.903 0.000 1.000 0.000  0
#&gt; SRR1946689     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1946686     3  0.0336      0.867 0.008 0.000 0.992  0
#&gt; SRR1946685     3  0.4431      0.587 0.000 0.304 0.696  0
#&gt; SRR1946688     2  0.0188      0.903 0.000 0.996 0.004  0
#&gt; SRR1946684     1  0.1545      0.849 0.952 0.040 0.008  0
#&gt; SRR1946683     3  0.0000      0.868 0.000 0.000 1.000  0
#&gt; SRR1946682     2  0.0336      0.901 0.000 0.992 0.008  0
#&gt; SRR1946680     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1946681     3  0.4916      0.312 0.000 0.424 0.576  0
#&gt; SRR1946687     3  0.0000      0.868 0.000 0.000 1.000  0
#&gt; SRR1946679     2  0.2921      0.874 0.000 0.860 0.140  0
#&gt; SRR1946678     1  0.0000      0.884 1.000 0.000 0.000  0
#&gt; SRR1946676     3  0.3764      0.713 0.000 0.216 0.784  0
#&gt; SRR1946677     3  0.6731      0.517 0.148 0.248 0.604  0
#&gt; SRR1946672     3  0.0376      0.868 0.004 0.004 0.992  0
#&gt; SRR1946673     2  0.3024      0.873 0.000 0.852 0.148  0
#&gt; SRR1946671     3  0.4050      0.772 0.036 0.144 0.820  0
#&gt; SRR1946669     1  0.0336      0.878 0.992 0.000 0.008  0
#&gt; SRR1946668     3  0.4008      0.671 0.244 0.000 0.756  0
#&gt; SRR1946666     3  0.0336      0.867 0.008 0.000 0.992  0
#&gt; SRR1946667     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1946670     3  0.2469      0.775 0.000 0.108 0.892  0
#&gt; SRR1946663     3  0.6868      0.462 0.120 0.336 0.544  0
#&gt; SRR1946664     2  0.0000      0.903 0.000 1.000 0.000  0
#&gt; SRR1946662     1  0.3933      0.668 0.792 0.200 0.008  0
#&gt; SRR1946661     2  0.2973      0.876 0.000 0.856 0.144  0
#&gt; SRR1946660     2  0.0188      0.903 0.000 0.996 0.004  0
#&gt; SRR1946659     1  0.0000      0.884 1.000 0.000 0.000  0
#&gt; SRR1946658     2  0.0469      0.902 0.000 0.988 0.012  0
#&gt; SRR1946657     2  0.2921      0.874 0.000 0.860 0.140  0
#&gt; SRR1946655     3  0.0336      0.868 0.000 0.008 0.992  0
#&gt; SRR1946654     3  0.0336      0.868 0.000 0.008 0.992  0
#&gt; SRR1946653     3  0.0336      0.867 0.008 0.000 0.992  0
#&gt; SRR1946652     2  0.2921      0.874 0.000 0.860 0.140  0
#&gt; SRR1946651     2  0.1557      0.901 0.000 0.944 0.056  0
#&gt; SRR1946650     2  0.0336      0.906 0.000 0.992 0.008  0
#&gt; SRR1946649     1  0.4222      0.580 0.728 0.272 0.000  0
#&gt; SRR1946648     3  0.0000      0.868 0.000 0.000 1.000  0
#&gt; SRR1946647     3  0.0188      0.867 0.004 0.000 0.996  0
#&gt; SRR1946646     3  0.0336      0.868 0.000 0.008 0.992  0
#&gt; SRR1946645     1  0.4855      0.204 0.600 0.000 0.400  0
#&gt; SRR1946644     2  0.2868      0.877 0.000 0.864 0.136  0
#&gt; SRR1946643     3  0.0336      0.868 0.000 0.008 0.992  0
#&gt; SRR1946642     1  0.0000      0.884 1.000 0.000 0.000  0
#&gt; SRR1946641     1  0.0000      0.884 1.000 0.000 0.000  0
#&gt; SRR1946656     3  0.0336      0.868 0.000 0.008 0.992  0
#&gt; SRR1946640     1  0.0000      0.884 1.000 0.000 0.000  0
#&gt; SRR1946639     1  0.0000      0.884 1.000 0.000 0.000  0
#&gt; SRR1946638     1  0.0000      0.884 1.000 0.000 0.000  0
#&gt; SRR1946637     1  0.0000      0.884 1.000 0.000 0.000  0
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5
#&gt; SRR1946675     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946691     2   0.445     0.3691 0.000 0.500 0.004  0 0.496
#&gt; SRR1946690     2   0.256     0.7671 0.000 0.856 0.000  0 0.144
#&gt; SRR1946689     4   0.000     1.0000 0.000 0.000 0.000  1 0.000
#&gt; SRR1946686     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946685     3   0.382     0.6122 0.000 0.304 0.696  0 0.000
#&gt; SRR1946688     2   0.431     0.3563 0.000 0.504 0.000  0 0.496
#&gt; SRR1946684     5   0.407     0.5467 0.300 0.008 0.000  0 0.692
#&gt; SRR1946683     3   0.389     0.4791 0.000 0.000 0.680  0 0.320
#&gt; SRR1946682     5   0.000     0.6918 0.000 0.000 0.000  0 1.000
#&gt; SRR1946680     4   0.000     1.0000 0.000 0.000 0.000  1 0.000
#&gt; SRR1946681     3   0.423     0.3875 0.000 0.424 0.576  0 0.000
#&gt; SRR1946687     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946679     2   0.000     0.8398 0.000 1.000 0.000  0 0.000
#&gt; SRR1946678     1   0.000     0.8476 1.000 0.000 0.000  0 0.000
#&gt; SRR1946676     3   0.321     0.7229 0.000 0.212 0.788  0 0.000
#&gt; SRR1946677     3   0.599    -0.0290 0.016 0.068 0.476  0 0.440
#&gt; SRR1946672     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946673     5   0.402     0.5477 0.000 0.348 0.000  0 0.652
#&gt; SRR1946671     3   0.383     0.7609 0.028 0.136 0.816  0 0.020
#&gt; SRR1946669     1   0.426     0.0528 0.564 0.000 0.000  0 0.436
#&gt; SRR1946668     5   0.478     0.6055 0.060 0.000 0.248  0 0.692
#&gt; SRR1946666     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946667     4   0.000     1.0000 0.000 0.000 0.000  1 0.000
#&gt; SRR1946670     5   0.173     0.6798 0.000 0.000 0.080  0 0.920
#&gt; SRR1946663     5   0.000     0.6918 0.000 0.000 0.000  0 1.000
#&gt; SRR1946664     2   0.000     0.8398 0.000 1.000 0.000  0 0.000
#&gt; SRR1946662     5   0.478     0.6003 0.248 0.060 0.000  0 0.692
#&gt; SRR1946661     5   0.382     0.5940 0.000 0.304 0.000  0 0.696
#&gt; SRR1946660     2   0.414     0.5576 0.000 0.616 0.000  0 0.384
#&gt; SRR1946659     1   0.000     0.8476 1.000 0.000 0.000  0 0.000
#&gt; SRR1946658     5   0.297     0.5944 0.000 0.168 0.004  0 0.828
#&gt; SRR1946657     2   0.000     0.8398 0.000 1.000 0.000  0 0.000
#&gt; SRR1946655     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946654     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946653     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946652     2   0.000     0.8398 0.000 1.000 0.000  0 0.000
#&gt; SRR1946651     2   0.000     0.8398 0.000 1.000 0.000  0 0.000
#&gt; SRR1946650     2   0.000     0.8398 0.000 1.000 0.000  0 0.000
#&gt; SRR1946649     1   0.366     0.5300 0.724 0.276 0.000  0 0.000
#&gt; SRR1946648     3   0.134     0.8316 0.000 0.000 0.944  0 0.056
#&gt; SRR1946647     5   0.384     0.5419 0.000 0.000 0.308  0 0.692
#&gt; SRR1946646     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946645     1   0.418     0.2242 0.600 0.000 0.400  0 0.000
#&gt; SRR1946644     2   0.000     0.8398 0.000 1.000 0.000  0 0.000
#&gt; SRR1946643     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946642     1   0.000     0.8476 1.000 0.000 0.000  0 0.000
#&gt; SRR1946641     1   0.000     0.8476 1.000 0.000 0.000  0 0.000
#&gt; SRR1946656     3   0.000     0.8658 0.000 0.000 1.000  0 0.000
#&gt; SRR1946640     1   0.000     0.8476 1.000 0.000 0.000  0 0.000
#&gt; SRR1946639     1   0.000     0.8476 1.000 0.000 0.000  0 0.000
#&gt; SRR1946638     1   0.000     0.8476 1.000 0.000 0.000  0 0.000
#&gt; SRR1946637     1   0.000     0.8476 1.000 0.000 0.000  0 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5    p6
#&gt; SRR1946675     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946691     6  0.0146     0.6793 0.000 0.000 0.000  0 0.004 0.996
#&gt; SRR1946690     6  0.3867    -0.0930 0.000 0.488 0.000  0 0.000 0.512
#&gt; SRR1946689     4  0.0000     1.0000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946686     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946685     3  0.3446     0.5346 0.000 0.308 0.692  0 0.000 0.000
#&gt; SRR1946688     6  0.0000     0.6785 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1946684     5  0.0000     0.8142 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946683     3  0.4868     0.3822 0.000 0.076 0.592  0 0.332 0.000
#&gt; SRR1946682     6  0.3446     0.4961 0.000 0.000 0.000  0 0.308 0.692
#&gt; SRR1946680     4  0.0000     1.0000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946681     3  0.3774     0.3120 0.000 0.408 0.592  0 0.000 0.000
#&gt; SRR1946687     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946679     2  0.0000     0.7489 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1946678     1  0.0000     0.9398 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946676     3  0.3843     0.3236 0.000 0.452 0.548  0 0.000 0.000
#&gt; SRR1946677     5  0.6306     0.0651 0.012 0.252 0.320  0 0.416 0.000
#&gt; SRR1946672     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946673     5  0.2178     0.7025 0.000 0.132 0.000  0 0.868 0.000
#&gt; SRR1946671     3  0.4821     0.4091 0.028 0.376 0.576  0 0.020 0.000
#&gt; SRR1946669     5  0.2762     0.6012 0.196 0.000 0.000  0 0.804 0.000
#&gt; SRR1946668     5  0.0146     0.8122 0.004 0.000 0.000  0 0.996 0.000
#&gt; SRR1946666     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946667     4  0.0000     1.0000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1946670     6  0.3897     0.5213 0.000 0.000 0.024  0 0.280 0.696
#&gt; SRR1946663     6  0.3076     0.5715 0.000 0.000 0.000  0 0.240 0.760
#&gt; SRR1946664     2  0.3101     0.5149 0.000 0.756 0.000  0 0.000 0.244
#&gt; SRR1946662     5  0.0000     0.8142 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946661     5  0.0000     0.8142 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946660     6  0.0000     0.6785 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1946659     1  0.0000     0.9398 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946658     6  0.5104     0.4487 0.000 0.108 0.000  0 0.304 0.588
#&gt; SRR1946657     2  0.3023     0.6136 0.000 0.768 0.232  0 0.000 0.000
#&gt; SRR1946655     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946654     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946653     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946652     2  0.0146     0.7469 0.000 0.996 0.000  0 0.004 0.000
#&gt; SRR1946651     2  0.0000     0.7489 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1946650     2  0.0000     0.7489 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1946649     2  0.3996    -0.0693 0.484 0.512 0.000  0 0.004 0.000
#&gt; SRR1946648     3  0.1814     0.7924 0.000 0.000 0.900  0 0.100 0.000
#&gt; SRR1946647     5  0.0000     0.8142 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1946646     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946645     1  0.5330     0.3908 0.592 0.232 0.176  0 0.000 0.000
#&gt; SRR1946644     2  0.3101     0.6024 0.000 0.756 0.244  0 0.000 0.000
#&gt; SRR1946643     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946642     1  0.0000     0.9398 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.9398 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946656     3  0.0000     0.8550 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR1946640     1  0.0000     0.9398 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.9398 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9398 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9398 1.000 0.000 0.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.365           0.669       0.773         0.3891 0.643   0.643
#> 3 3 0.172           0.283       0.617         0.3306 0.556   0.441
#> 4 4 0.571           0.810       0.892         0.1175 0.767   0.590
#> 5 5 0.474           0.602       0.773         0.2258 0.840   0.615
#> 6 6 0.656           0.624       0.762         0.0995 0.959   0.856
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     1  0.9580      0.613 0.620 0.380
#&gt; SRR1946691     2  0.9954      0.824 0.460 0.540
#&gt; SRR1946690     2  0.9993      0.803 0.484 0.516
#&gt; SRR1946689     2  0.5178      0.518 0.116 0.884
#&gt; SRR1946686     1  0.9580      0.613 0.620 0.380
#&gt; SRR1946685     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946688     2  0.9954      0.824 0.460 0.540
#&gt; SRR1946684     1  0.6048      0.425 0.852 0.148
#&gt; SRR1946683     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946682     2  0.9954      0.824 0.460 0.540
#&gt; SRR1946680     2  0.5294      0.517 0.120 0.880
#&gt; SRR1946681     1  0.0938      0.700 0.988 0.012
#&gt; SRR1946687     1  0.9323      0.628 0.652 0.348
#&gt; SRR1946679     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946678     1  0.3879      0.653 0.924 0.076
#&gt; SRR1946676     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946677     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946672     1  0.9286      0.630 0.656 0.344
#&gt; SRR1946673     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946671     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946669     1  0.0376      0.698 0.996 0.004
#&gt; SRR1946668     1  0.0672      0.696 0.992 0.008
#&gt; SRR1946666     1  0.9580      0.613 0.620 0.380
#&gt; SRR1946667     2  0.5178      0.518 0.116 0.884
#&gt; SRR1946670     2  0.9954      0.824 0.460 0.540
#&gt; SRR1946663     2  0.9954      0.824 0.460 0.540
#&gt; SRR1946664     2  0.9993      0.803 0.484 0.516
#&gt; SRR1946662     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946661     1  0.0938      0.691 0.988 0.012
#&gt; SRR1946660     2  0.9954      0.824 0.460 0.540
#&gt; SRR1946659     1  0.9552      0.615 0.624 0.376
#&gt; SRR1946658     2  0.9988      0.805 0.480 0.520
#&gt; SRR1946657     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946655     1  0.9286      0.630 0.656 0.344
#&gt; SRR1946654     1  0.9286      0.630 0.656 0.344
#&gt; SRR1946653     1  0.9580      0.613 0.620 0.380
#&gt; SRR1946652     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946651     1  0.2778      0.636 0.952 0.048
#&gt; SRR1946650     1  0.1184      0.682 0.984 0.016
#&gt; SRR1946649     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946648     1  0.8909      0.640 0.692 0.308
#&gt; SRR1946647     1  0.0672      0.696 0.992 0.008
#&gt; SRR1946646     1  0.2236      0.698 0.964 0.036
#&gt; SRR1946645     1  0.0000      0.699 1.000 0.000
#&gt; SRR1946644     1  0.3431      0.614 0.936 0.064
#&gt; SRR1946643     1  0.9286      0.630 0.656 0.344
#&gt; SRR1946642     1  0.3879      0.653 0.924 0.076
#&gt; SRR1946641     1  0.9944      0.552 0.544 0.456
#&gt; SRR1946656     1  0.9286      0.630 0.656 0.344
#&gt; SRR1946640     1  0.9909      0.566 0.556 0.444
#&gt; SRR1946639     1  0.9815      0.581 0.580 0.420
#&gt; SRR1946638     1  0.9944      0.552 0.544 0.456
#&gt; SRR1946637     1  0.9944      0.552 0.544 0.456
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     2  0.9424   -0.13549 0.352 0.464 0.184
#&gt; SRR1946691     3  0.6495   -0.19646 0.004 0.460 0.536
#&gt; SRR1946690     2  0.6252    0.13472 0.000 0.556 0.444
#&gt; SRR1946689     3  0.5335    0.22258 0.232 0.008 0.760
#&gt; SRR1946686     1  0.9111    0.29177 0.472 0.384 0.144
#&gt; SRR1946685     2  0.0237    0.57638 0.004 0.996 0.000
#&gt; SRR1946688     3  0.6309   -0.25431 0.000 0.496 0.504
#&gt; SRR1946684     2  0.8230    0.29408 0.088 0.564 0.348
#&gt; SRR1946683     2  0.2878    0.53793 0.096 0.904 0.000
#&gt; SRR1946682     2  0.6295    0.08771 0.000 0.528 0.472
#&gt; SRR1946680     1  0.9191   -0.03096 0.432 0.148 0.420
#&gt; SRR1946681     2  0.5327    0.44806 0.000 0.728 0.272
#&gt; SRR1946687     1  0.9714    0.14193 0.420 0.224 0.356
#&gt; SRR1946679     2  0.0000    0.57813 0.000 1.000 0.000
#&gt; SRR1946678     1  0.6291    0.20741 0.532 0.468 0.000
#&gt; SRR1946676     2  0.0475    0.57811 0.004 0.992 0.004
#&gt; SRR1946677     2  0.2448    0.55287 0.076 0.924 0.000
#&gt; SRR1946672     2  0.9203   -0.09667 0.248 0.536 0.216
#&gt; SRR1946673     2  0.2356    0.55545 0.072 0.928 0.000
#&gt; SRR1946671     2  0.0424    0.57431 0.008 0.992 0.000
#&gt; SRR1946669     2  0.7394    0.21522 0.284 0.652 0.064
#&gt; SRR1946668     2  0.8067    0.36029 0.100 0.616 0.284
#&gt; SRR1946666     2  0.9579   -0.17025 0.352 0.444 0.204
#&gt; SRR1946667     3  0.5335    0.22258 0.232 0.008 0.760
#&gt; SRR1946670     2  0.6305    0.05266 0.000 0.516 0.484
#&gt; SRR1946663     2  0.6299    0.07854 0.000 0.524 0.476
#&gt; SRR1946664     2  0.6267    0.11817 0.000 0.548 0.452
#&gt; SRR1946662     2  0.4768    0.54373 0.100 0.848 0.052
#&gt; SRR1946661     2  0.7485    0.40027 0.096 0.680 0.224
#&gt; SRR1946660     2  0.6299    0.07854 0.000 0.524 0.476
#&gt; SRR1946659     2  0.9674   -0.27323 0.392 0.396 0.212
#&gt; SRR1946658     2  0.7890    0.26852 0.064 0.564 0.372
#&gt; SRR1946657     2  0.2711    0.57185 0.000 0.912 0.088
#&gt; SRR1946655     1  0.9648    0.19576 0.460 0.304 0.236
#&gt; SRR1946654     2  0.9203   -0.09667 0.248 0.536 0.216
#&gt; SRR1946653     1  0.9651    0.21533 0.436 0.348 0.216
#&gt; SRR1946652     2  0.0237    0.57948 0.000 0.996 0.004
#&gt; SRR1946651     2  0.1411    0.58560 0.000 0.964 0.036
#&gt; SRR1946650     2  0.0747    0.58152 0.000 0.984 0.016
#&gt; SRR1946649     2  0.0237    0.57638 0.004 0.996 0.000
#&gt; SRR1946648     2  0.8955   -0.00933 0.332 0.524 0.144
#&gt; SRR1946647     2  0.8390    0.31004 0.100 0.560 0.340
#&gt; SRR1946646     2  0.5507    0.50607 0.056 0.808 0.136
#&gt; SRR1946645     2  0.1860    0.56461 0.052 0.948 0.000
#&gt; SRR1946644     2  0.6008    0.25396 0.000 0.628 0.372
#&gt; SRR1946643     1  0.9722    0.20345 0.444 0.312 0.244
#&gt; SRR1946642     1  0.6302    0.18164 0.520 0.480 0.000
#&gt; SRR1946641     1  0.4931    0.53364 0.768 0.232 0.000
#&gt; SRR1946656     1  0.9671    0.17520 0.460 0.292 0.248
#&gt; SRR1946640     1  0.4931    0.53364 0.768 0.232 0.000
#&gt; SRR1946639     1  0.4974    0.53191 0.764 0.236 0.000
#&gt; SRR1946638     1  0.4931    0.53364 0.768 0.232 0.000
#&gt; SRR1946637     1  0.4931    0.53364 0.768 0.232 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.3879     0.8339 0.024 0.128 0.840 0.008
#&gt; SRR1946691     2  0.2853     0.9004 0.008 0.900 0.076 0.016
#&gt; SRR1946690     2  0.2597     0.9007 0.008 0.904 0.084 0.004
#&gt; SRR1946689     4  0.1867     0.8555 0.000 0.000 0.072 0.928
#&gt; SRR1946686     1  0.7075    -0.0177 0.488 0.128 0.384 0.000
#&gt; SRR1946685     2  0.1209     0.9215 0.004 0.964 0.032 0.000
#&gt; SRR1946688     2  0.2732     0.9024 0.008 0.904 0.076 0.012
#&gt; SRR1946684     2  0.2441     0.9077 0.012 0.916 0.068 0.004
#&gt; SRR1946683     2  0.1356     0.9211 0.008 0.960 0.032 0.000
#&gt; SRR1946682     2  0.2732     0.9027 0.012 0.904 0.076 0.008
#&gt; SRR1946680     4  0.5610     0.6536 0.004 0.068 0.216 0.712
#&gt; SRR1946681     2  0.2944     0.8986 0.000 0.868 0.128 0.004
#&gt; SRR1946687     3  0.4854     0.8177 0.052 0.136 0.796 0.016
#&gt; SRR1946679     2  0.1209     0.9215 0.004 0.964 0.032 0.000
#&gt; SRR1946678     1  0.4250     0.5088 0.724 0.276 0.000 0.000
#&gt; SRR1946676     2  0.1209     0.9215 0.004 0.964 0.032 0.000
#&gt; SRR1946677     2  0.1356     0.9211 0.008 0.960 0.032 0.000
#&gt; SRR1946672     3  0.3142     0.8318 0.000 0.132 0.860 0.008
#&gt; SRR1946673     2  0.1356     0.9211 0.008 0.960 0.032 0.000
#&gt; SRR1946671     2  0.1209     0.9215 0.004 0.964 0.032 0.000
#&gt; SRR1946669     2  0.4632     0.4365 0.308 0.688 0.004 0.000
#&gt; SRR1946668     2  0.0779     0.9167 0.016 0.980 0.004 0.000
#&gt; SRR1946666     3  0.4621     0.8161 0.076 0.128 0.796 0.000
#&gt; SRR1946667     4  0.1867     0.8555 0.000 0.000 0.072 0.928
#&gt; SRR1946670     2  0.2732     0.9024 0.008 0.904 0.076 0.012
#&gt; SRR1946663     2  0.2732     0.9024 0.008 0.904 0.076 0.012
#&gt; SRR1946664     2  0.2597     0.9007 0.008 0.904 0.084 0.004
#&gt; SRR1946662     2  0.0524     0.9172 0.008 0.988 0.004 0.000
#&gt; SRR1946661     2  0.0376     0.9171 0.004 0.992 0.004 0.000
#&gt; SRR1946660     2  0.2708     0.9029 0.016 0.904 0.076 0.004
#&gt; SRR1946659     3  0.4336     0.8253 0.060 0.128 0.812 0.000
#&gt; SRR1946658     2  0.2790     0.9032 0.012 0.904 0.072 0.012
#&gt; SRR1946657     2  0.1305     0.9222 0.004 0.960 0.036 0.000
#&gt; SRR1946655     3  0.2530     0.6332 0.000 0.004 0.896 0.100
#&gt; SRR1946654     3  0.3271     0.8308 0.000 0.132 0.856 0.012
#&gt; SRR1946653     3  0.3447     0.8340 0.020 0.128 0.852 0.000
#&gt; SRR1946652     2  0.1209     0.9215 0.004 0.964 0.032 0.000
#&gt; SRR1946651     2  0.1209     0.9215 0.004 0.964 0.032 0.000
#&gt; SRR1946650     2  0.1209     0.9215 0.004 0.964 0.032 0.000
#&gt; SRR1946649     2  0.1109     0.9218 0.004 0.968 0.028 0.000
#&gt; SRR1946648     3  0.4589     0.7505 0.024 0.188 0.780 0.008
#&gt; SRR1946647     2  0.1975     0.9123 0.048 0.936 0.016 0.000
#&gt; SRR1946646     2  0.4277     0.6877 0.000 0.720 0.280 0.000
#&gt; SRR1946645     2  0.1356     0.9211 0.008 0.960 0.032 0.000
#&gt; SRR1946644     2  0.2831     0.9015 0.000 0.876 0.120 0.004
#&gt; SRR1946643     3  0.2466     0.6367 0.000 0.004 0.900 0.096
#&gt; SRR1946642     1  0.4543     0.4509 0.676 0.324 0.000 0.000
#&gt; SRR1946641     1  0.0336     0.7191 0.992 0.000 0.008 0.000
#&gt; SRR1946656     3  0.2530     0.6332 0.000 0.004 0.896 0.100
#&gt; SRR1946640     1  0.0469     0.7155 0.988 0.000 0.012 0.000
#&gt; SRR1946639     1  0.0927     0.7149 0.976 0.016 0.008 0.000
#&gt; SRR1946638     1  0.0524     0.7192 0.988 0.004 0.008 0.000
#&gt; SRR1946637     1  0.0336     0.7191 0.992 0.000 0.008 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.6350   0.670727 0.192 0.048 0.628 0.000 0.132
#&gt; SRR1946691     2  0.3421   0.904939 0.000 0.788 0.008 0.000 0.204
#&gt; SRR1946690     5  0.5108  -0.137998 0.000 0.420 0.008 0.024 0.548
#&gt; SRR1946689     4  0.0510   0.682309 0.000 0.016 0.000 0.984 0.000
#&gt; SRR1946686     3  0.7035   0.597795 0.376 0.044 0.448 0.000 0.132
#&gt; SRR1946685     5  0.1243   0.706630 0.000 0.028 0.004 0.008 0.960
#&gt; SRR1946688     2  0.3266   0.912719 0.000 0.796 0.000 0.004 0.200
#&gt; SRR1946684     5  0.5718  -0.000667 0.028 0.396 0.028 0.004 0.544
#&gt; SRR1946683     5  0.3430   0.615485 0.000 0.220 0.000 0.004 0.776
#&gt; SRR1946682     2  0.3333   0.912085 0.000 0.788 0.000 0.004 0.208
#&gt; SRR1946680     4  0.8031   0.060032 0.000 0.200 0.236 0.432 0.132
#&gt; SRR1946681     5  0.5492   0.153837 0.000 0.324 0.040 0.024 0.612
#&gt; SRR1946687     3  0.7400   0.575377 0.384 0.052 0.424 0.008 0.132
#&gt; SRR1946679     5  0.1168   0.707316 0.000 0.032 0.000 0.008 0.960
#&gt; SRR1946678     1  0.1124   0.934798 0.960 0.004 0.000 0.000 0.036
#&gt; SRR1946676     5  0.1618   0.702478 0.000 0.040 0.008 0.008 0.944
#&gt; SRR1946677     5  0.3300   0.607584 0.000 0.204 0.000 0.004 0.792
#&gt; SRR1946672     3  0.3578   0.599138 0.000 0.048 0.820 0.000 0.132
#&gt; SRR1946673     5  0.0955   0.699856 0.000 0.028 0.000 0.004 0.968
#&gt; SRR1946671     5  0.3266   0.608084 0.000 0.200 0.000 0.004 0.796
#&gt; SRR1946669     5  0.2548   0.647829 0.004 0.116 0.000 0.004 0.876
#&gt; SRR1946668     5  0.5504   0.146265 0.028 0.344 0.032 0.000 0.596
#&gt; SRR1946666     3  0.7043   0.590240 0.384 0.044 0.440 0.000 0.132
#&gt; SRR1946667     4  0.0510   0.682309 0.000 0.016 0.000 0.984 0.000
#&gt; SRR1946670     2  0.3266   0.912719 0.000 0.796 0.000 0.004 0.200
#&gt; SRR1946663     2  0.3333   0.912085 0.000 0.788 0.000 0.004 0.208
#&gt; SRR1946664     2  0.4698   0.321998 0.000 0.520 0.008 0.004 0.468
#&gt; SRR1946662     5  0.1571   0.700628 0.000 0.060 0.000 0.004 0.936
#&gt; SRR1946661     5  0.1731   0.693526 0.004 0.060 0.000 0.004 0.932
#&gt; SRR1946660     2  0.3266   0.912719 0.000 0.796 0.000 0.004 0.200
#&gt; SRR1946659     3  0.7043   0.590240 0.384 0.044 0.440 0.000 0.132
#&gt; SRR1946658     5  0.5092  -0.245737 0.000 0.464 0.012 0.016 0.508
#&gt; SRR1946657     5  0.1914   0.690217 0.000 0.056 0.008 0.008 0.928
#&gt; SRR1946655     3  0.0613   0.453823 0.004 0.008 0.984 0.004 0.000
#&gt; SRR1946654     3  0.3735   0.600046 0.004 0.048 0.816 0.000 0.132
#&gt; SRR1946653     3  0.6515   0.670695 0.216 0.048 0.604 0.000 0.132
#&gt; SRR1946652     5  0.1490   0.704227 0.004 0.032 0.004 0.008 0.952
#&gt; SRR1946651     5  0.1638   0.689332 0.000 0.064 0.004 0.000 0.932
#&gt; SRR1946650     5  0.0703   0.706795 0.000 0.024 0.000 0.000 0.976
#&gt; SRR1946649     5  0.2377   0.650523 0.000 0.128 0.000 0.000 0.872
#&gt; SRR1946648     3  0.6569   0.669534 0.200 0.056 0.608 0.000 0.136
#&gt; SRR1946647     5  0.6558   0.083425 0.088 0.320 0.048 0.000 0.544
#&gt; SRR1946646     3  0.5693   0.232214 0.004 0.068 0.488 0.000 0.440
#&gt; SRR1946645     5  0.3352   0.614115 0.004 0.192 0.000 0.004 0.800
#&gt; SRR1946644     5  0.5503   0.244043 0.000 0.272 0.092 0.004 0.632
#&gt; SRR1946643     3  0.0693   0.449171 0.000 0.008 0.980 0.012 0.000
#&gt; SRR1946642     1  0.2830   0.839207 0.876 0.080 0.000 0.000 0.044
#&gt; SRR1946641     1  0.0162   0.958788 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946656     3  0.0693   0.449171 0.000 0.008 0.980 0.012 0.000
#&gt; SRR1946640     1  0.0290   0.951858 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1946639     1  0.0671   0.953520 0.980 0.004 0.000 0.000 0.016
#&gt; SRR1946638     1  0.0162   0.958788 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946637     1  0.0162   0.958788 0.996 0.000 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.3603     0.6238 0.072 NA 0.808 0.000 0.008 0.000
#&gt; SRR1946691     6  0.3136     0.7525 0.000 NA 0.020 0.000 0.108 0.844
#&gt; SRR1946690     6  0.6638     0.5024 0.000 NA 0.044 0.000 0.272 0.452
#&gt; SRR1946689     4  0.0000     0.7645 0.000 NA 0.000 1.000 0.000 0.000
#&gt; SRR1946686     3  0.5968     0.4153 0.356 NA 0.460 0.000 0.008 0.000
#&gt; SRR1946685     5  0.2398     0.7331 0.000 NA 0.020 0.000 0.876 0.000
#&gt; SRR1946688     6  0.1663     0.7707 0.000 NA 0.000 0.000 0.088 0.912
#&gt; SRR1946684     5  0.6464     0.1206 0.004 NA 0.040 0.000 0.460 0.348
#&gt; SRR1946683     5  0.3930     0.7130 0.000 NA 0.016 0.000 0.788 0.076
#&gt; SRR1946682     6  0.1753     0.7677 0.000 NA 0.000 0.000 0.084 0.912
#&gt; SRR1946680     4  0.7615     0.3870 0.000 NA 0.192 0.452 0.068 0.060
#&gt; SRR1946681     5  0.7068     0.2181 0.000 NA 0.136 0.016 0.456 0.084
#&gt; SRR1946687     3  0.6144     0.4374 0.320 NA 0.444 0.000 0.008 0.000
#&gt; SRR1946679     5  0.1625     0.7384 0.000 NA 0.012 0.000 0.928 0.000
#&gt; SRR1946678     1  0.3423     0.7791 0.812 NA 0.000 0.000 0.088 0.000
#&gt; SRR1946676     5  0.2398     0.7331 0.000 NA 0.020 0.000 0.876 0.000
#&gt; SRR1946677     5  0.3361     0.7152 0.000 NA 0.000 0.000 0.816 0.076
#&gt; SRR1946672     3  0.0520     0.6174 0.000 NA 0.984 0.000 0.008 0.000
#&gt; SRR1946673     5  0.1957     0.7389 0.000 NA 0.000 0.000 0.888 0.000
#&gt; SRR1946671     5  0.3219     0.7205 0.000 NA 0.008 0.000 0.840 0.076
#&gt; SRR1946669     5  0.3643     0.6919 0.008 NA 0.024 0.000 0.768 0.000
#&gt; SRR1946668     5  0.6816     0.3122 0.016 NA 0.040 0.000 0.484 0.244
#&gt; SRR1946666     3  0.6004     0.4176 0.352 NA 0.456 0.000 0.008 0.000
#&gt; SRR1946667     4  0.0000     0.7645 0.000 NA 0.000 1.000 0.000 0.000
#&gt; SRR1946670     6  0.1970     0.7713 0.008 NA 0.000 0.000 0.092 0.900
#&gt; SRR1946663     6  0.2001     0.7714 0.000 NA 0.004 0.000 0.092 0.900
#&gt; SRR1946664     6  0.6503     0.5262 0.000 NA 0.044 0.000 0.212 0.488
#&gt; SRR1946662     5  0.3301     0.6999 0.000 NA 0.024 0.000 0.788 0.000
#&gt; SRR1946661     5  0.3202     0.7065 0.000 NA 0.024 0.000 0.800 0.000
#&gt; SRR1946660     6  0.1918     0.7697 0.008 NA 0.000 0.000 0.088 0.904
#&gt; SRR1946659     3  0.6004     0.4176 0.352 NA 0.456 0.000 0.008 0.000
#&gt; SRR1946658     6  0.6719     0.3216 0.000 NA 0.032 0.000 0.300 0.336
#&gt; SRR1946657     5  0.2063     0.7345 0.000 NA 0.020 0.000 0.912 0.008
#&gt; SRR1946655     3  0.1957     0.5747 0.000 NA 0.888 0.000 0.000 0.000
#&gt; SRR1946654     3  0.0547     0.6152 0.000 NA 0.980 0.000 0.020 0.000
#&gt; SRR1946653     3  0.3802     0.6222 0.084 NA 0.792 0.000 0.008 0.000
#&gt; SRR1946652     5  0.2039     0.7348 0.000 NA 0.020 0.000 0.904 0.000
#&gt; SRR1946651     5  0.3411     0.7075 0.000 NA 0.024 0.000 0.804 0.012
#&gt; SRR1946650     5  0.2709     0.7199 0.000 NA 0.020 0.000 0.848 0.000
#&gt; SRR1946649     5  0.2434     0.7343 0.000 NA 0.008 0.000 0.892 0.064
#&gt; SRR1946648     3  0.5132     0.5727 0.100 NA 0.716 0.000 0.068 0.004
#&gt; SRR1946647     5  0.7589     0.2459 0.052 NA 0.068 0.000 0.444 0.200
#&gt; SRR1946646     3  0.6176    -0.0269 0.000 NA 0.440 0.000 0.360 0.016
#&gt; SRR1946645     5  0.3850     0.7176 0.004 NA 0.016 0.000 0.804 0.076
#&gt; SRR1946644     5  0.6845     0.2293 0.000 NA 0.140 0.000 0.472 0.108
#&gt; SRR1946643     3  0.2053     0.5735 0.000 NA 0.888 0.004 0.000 0.000
#&gt; SRR1946642     1  0.3372     0.7845 0.816 NA 0.000 0.000 0.084 0.000
#&gt; SRR1946641     1  0.0000     0.9104 1.000 NA 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.2053     0.5735 0.000 NA 0.888 0.004 0.000 0.000
#&gt; SRR1946640     1  0.0547     0.8983 0.980 NA 0.020 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0363     0.9066 0.988 NA 0.000 0.000 0.012 0.000
#&gt; SRR1946638     1  0.0000     0.9104 1.000 NA 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9104 1.000 NA 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.611           0.806       0.918         0.4911 0.495   0.495
#> 3 3 0.764           0.849       0.931         0.2994 0.641   0.414
#> 4 4 0.557           0.707       0.841         0.1607 0.763   0.447
#> 5 5 0.784           0.764       0.884         0.0780 0.835   0.470
#> 6 6 0.739           0.578       0.798         0.0494 0.890   0.544
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2   0.990      0.318 0.440 0.560
#&gt; SRR1946691     2   0.000      0.880 0.000 1.000
#&gt; SRR1946690     2   0.000      0.880 0.000 1.000
#&gt; SRR1946689     2   0.000      0.880 0.000 1.000
#&gt; SRR1946686     1   0.000      0.927 1.000 0.000
#&gt; SRR1946685     2   0.946      0.509 0.364 0.636
#&gt; SRR1946688     2   0.000      0.880 0.000 1.000
#&gt; SRR1946684     1   0.000      0.927 1.000 0.000
#&gt; SRR1946683     1   0.000      0.927 1.000 0.000
#&gt; SRR1946682     2   0.625      0.786 0.156 0.844
#&gt; SRR1946680     2   0.000      0.880 0.000 1.000
#&gt; SRR1946681     2   0.000      0.880 0.000 1.000
#&gt; SRR1946687     1   0.963      0.277 0.612 0.388
#&gt; SRR1946679     2   0.886      0.618 0.304 0.696
#&gt; SRR1946678     1   0.000      0.927 1.000 0.000
#&gt; SRR1946676     2   0.745      0.735 0.212 0.788
#&gt; SRR1946677     1   0.000      0.927 1.000 0.000
#&gt; SRR1946672     2   0.917      0.572 0.332 0.668
#&gt; SRR1946673     1   0.730      0.696 0.796 0.204
#&gt; SRR1946671     1   0.000      0.927 1.000 0.000
#&gt; SRR1946669     1   0.000      0.927 1.000 0.000
#&gt; SRR1946668     1   0.000      0.927 1.000 0.000
#&gt; SRR1946666     1   0.000      0.927 1.000 0.000
#&gt; SRR1946667     2   0.000      0.880 0.000 1.000
#&gt; SRR1946670     2   0.000      0.880 0.000 1.000
#&gt; SRR1946663     2   0.921      0.565 0.336 0.664
#&gt; SRR1946664     2   0.000      0.880 0.000 1.000
#&gt; SRR1946662     1   0.000      0.927 1.000 0.000
#&gt; SRR1946661     1   0.833      0.591 0.736 0.264
#&gt; SRR1946660     2   0.000      0.880 0.000 1.000
#&gt; SRR1946659     1   0.000      0.927 1.000 0.000
#&gt; SRR1946658     2   0.000      0.880 0.000 1.000
#&gt; SRR1946657     2   0.000      0.880 0.000 1.000
#&gt; SRR1946655     2   0.000      0.880 0.000 1.000
#&gt; SRR1946654     2   0.224      0.866 0.036 0.964
#&gt; SRR1946653     2   0.781      0.714 0.232 0.768
#&gt; SRR1946652     2   0.311      0.857 0.056 0.944
#&gt; SRR1946651     2   0.000      0.880 0.000 1.000
#&gt; SRR1946650     2   0.997      0.229 0.468 0.532
#&gt; SRR1946649     1   0.000      0.927 1.000 0.000
#&gt; SRR1946648     1   0.983      0.146 0.576 0.424
#&gt; SRR1946647     1   0.494      0.824 0.892 0.108
#&gt; SRR1946646     2   0.242      0.865 0.040 0.960
#&gt; SRR1946645     1   0.000      0.927 1.000 0.000
#&gt; SRR1946644     2   0.000      0.880 0.000 1.000
#&gt; SRR1946643     2   0.000      0.880 0.000 1.000
#&gt; SRR1946642     1   0.000      0.927 1.000 0.000
#&gt; SRR1946641     1   0.000      0.927 1.000 0.000
#&gt; SRR1946656     2   0.000      0.880 0.000 1.000
#&gt; SRR1946640     1   0.000      0.927 1.000 0.000
#&gt; SRR1946639     1   0.000      0.927 1.000 0.000
#&gt; SRR1946638     1   0.000      0.927 1.000 0.000
#&gt; SRR1946637     1   0.000      0.927 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.5760      0.504 0.328 0.000 0.672
#&gt; SRR1946691     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946690     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946689     3  0.0000      0.939 0.000 0.000 1.000
#&gt; SRR1946686     1  0.0237      0.948 0.996 0.000 0.004
#&gt; SRR1946685     2  0.0592      0.896 0.012 0.988 0.000
#&gt; SRR1946688     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946684     2  0.5859      0.538 0.344 0.656 0.000
#&gt; SRR1946683     1  0.1860      0.915 0.948 0.052 0.000
#&gt; SRR1946682     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946680     3  0.0592      0.932 0.000 0.012 0.988
#&gt; SRR1946681     2  0.0592      0.892 0.000 0.988 0.012
#&gt; SRR1946687     3  0.3116      0.864 0.108 0.000 0.892
#&gt; SRR1946679     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946678     1  0.0000      0.950 1.000 0.000 0.000
#&gt; SRR1946676     2  0.0237      0.897 0.004 0.996 0.000
#&gt; SRR1946677     2  0.4555      0.757 0.200 0.800 0.000
#&gt; SRR1946672     3  0.1031      0.929 0.024 0.000 0.976
#&gt; SRR1946673     2  0.2796      0.853 0.092 0.908 0.000
#&gt; SRR1946671     2  0.6244      0.317 0.440 0.560 0.000
#&gt; SRR1946669     1  0.0237      0.949 0.996 0.004 0.000
#&gt; SRR1946668     2  0.6286      0.243 0.464 0.536 0.000
#&gt; SRR1946666     1  0.0892      0.938 0.980 0.000 0.020
#&gt; SRR1946667     3  0.0000      0.939 0.000 0.000 1.000
#&gt; SRR1946670     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946663     2  0.1163      0.890 0.028 0.972 0.000
#&gt; SRR1946664     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946662     2  0.4555      0.757 0.200 0.800 0.000
#&gt; SRR1946661     2  0.0892      0.893 0.020 0.980 0.000
#&gt; SRR1946660     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946659     1  0.2625      0.885 0.916 0.000 0.084
#&gt; SRR1946658     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946657     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946655     3  0.0000      0.939 0.000 0.000 1.000
#&gt; SRR1946654     3  0.0000      0.939 0.000 0.000 1.000
#&gt; SRR1946653     3  0.2625      0.887 0.084 0.000 0.916
#&gt; SRR1946652     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946651     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1946650     2  0.0747      0.895 0.016 0.984 0.000
#&gt; SRR1946649     2  0.4002      0.799 0.160 0.840 0.000
#&gt; SRR1946648     1  0.6303      0.629 0.720 0.032 0.248
#&gt; SRR1946647     1  0.3267      0.841 0.884 0.116 0.000
#&gt; SRR1946646     2  0.6434      0.377 0.008 0.612 0.380
#&gt; SRR1946645     1  0.1643      0.922 0.956 0.044 0.000
#&gt; SRR1946644     2  0.3340      0.808 0.000 0.880 0.120
#&gt; SRR1946643     3  0.0000      0.939 0.000 0.000 1.000
#&gt; SRR1946642     1  0.0000      0.950 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000      0.950 1.000 0.000 0.000
#&gt; SRR1946656     3  0.0000      0.939 0.000 0.000 1.000
#&gt; SRR1946640     1  0.0000      0.950 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.950 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.950 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.950 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.5397     0.5347 0.212 0.068 0.720 0.000
#&gt; SRR1946691     4  0.5989     0.4726 0.000 0.264 0.080 0.656
#&gt; SRR1946690     2  0.2921     0.7625 0.000 0.860 0.000 0.140
#&gt; SRR1946689     3  0.3801     0.7098 0.000 0.000 0.780 0.220
#&gt; SRR1946686     1  0.2589     0.8105 0.884 0.000 0.116 0.000
#&gt; SRR1946685     2  0.0000     0.8052 0.000 1.000 0.000 0.000
#&gt; SRR1946688     4  0.0000     0.7652 0.000 0.000 0.000 1.000
#&gt; SRR1946684     4  0.3982     0.7775 0.220 0.004 0.000 0.776
#&gt; SRR1946683     1  0.2089     0.8298 0.932 0.020 0.000 0.048
#&gt; SRR1946682     4  0.0376     0.7698 0.004 0.004 0.000 0.992
#&gt; SRR1946680     3  0.3764     0.7132 0.000 0.000 0.784 0.216
#&gt; SRR1946681     2  0.0188     0.8035 0.000 0.996 0.004 0.000
#&gt; SRR1946687     3  0.2813     0.7388 0.024 0.000 0.896 0.080
#&gt; SRR1946679     2  0.0336     0.8057 0.000 0.992 0.000 0.008
#&gt; SRR1946678     1  0.0000     0.8684 1.000 0.000 0.000 0.000
#&gt; SRR1946676     2  0.0000     0.8052 0.000 1.000 0.000 0.000
#&gt; SRR1946677     4  0.7285     0.4866 0.176 0.308 0.000 0.516
#&gt; SRR1946672     1  0.7137     0.3762 0.544 0.168 0.288 0.000
#&gt; SRR1946673     4  0.5159     0.7656 0.088 0.156 0.000 0.756
#&gt; SRR1946671     1  0.5110     0.6656 0.764 0.104 0.000 0.132
#&gt; SRR1946669     4  0.4800     0.6404 0.340 0.004 0.000 0.656
#&gt; SRR1946668     4  0.3569     0.7863 0.196 0.000 0.000 0.804
#&gt; SRR1946666     1  0.2408     0.8210 0.896 0.000 0.104 0.000
#&gt; SRR1946667     3  0.3764     0.7132 0.000 0.000 0.784 0.216
#&gt; SRR1946670     4  0.0000     0.7652 0.000 0.000 0.000 1.000
#&gt; SRR1946663     4  0.0188     0.7677 0.004 0.000 0.000 0.996
#&gt; SRR1946664     2  0.3074     0.7541 0.000 0.848 0.000 0.152
#&gt; SRR1946662     4  0.4574     0.7744 0.220 0.024 0.000 0.756
#&gt; SRR1946661     4  0.4662     0.7914 0.092 0.112 0.000 0.796
#&gt; SRR1946660     4  0.1940     0.7762 0.000 0.076 0.000 0.924
#&gt; SRR1946659     1  0.3801     0.7094 0.780 0.000 0.220 0.000
#&gt; SRR1946658     4  0.3764     0.7105 0.000 0.216 0.000 0.784
#&gt; SRR1946657     2  0.0000     0.8052 0.000 1.000 0.000 0.000
#&gt; SRR1946655     3  0.3400     0.6283 0.000 0.180 0.820 0.000
#&gt; SRR1946654     2  0.7315     0.2126 0.252 0.532 0.216 0.000
#&gt; SRR1946653     3  0.2589     0.6665 0.116 0.000 0.884 0.000
#&gt; SRR1946652     2  0.3074     0.7557 0.000 0.848 0.000 0.152
#&gt; SRR1946651     2  0.2469     0.7805 0.000 0.892 0.000 0.108
#&gt; SRR1946650     2  0.3873     0.6490 0.000 0.772 0.000 0.228
#&gt; SRR1946649     2  0.6936     0.4640 0.284 0.568 0.000 0.148
#&gt; SRR1946648     1  0.7775     0.5373 0.604 0.144 0.184 0.068
#&gt; SRR1946647     4  0.4155     0.7544 0.240 0.004 0.000 0.756
#&gt; SRR1946646     2  0.2412     0.7378 0.008 0.908 0.084 0.000
#&gt; SRR1946645     1  0.1118     0.8559 0.964 0.036 0.000 0.000
#&gt; SRR1946644     2  0.0188     0.8047 0.000 0.996 0.000 0.004
#&gt; SRR1946643     2  0.4661     0.3532 0.000 0.652 0.348 0.000
#&gt; SRR1946642     1  0.0000     0.8684 1.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.8684 1.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.4998    -0.0383 0.000 0.488 0.512 0.000
#&gt; SRR1946640     1  0.0592     0.8647 0.984 0.000 0.016 0.000
#&gt; SRR1946639     1  0.0000     0.8684 1.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.8684 1.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.8684 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.1670     0.8187 0.000 0.000 0.936 0.012 0.052
#&gt; SRR1946691     2  0.4415     0.3580 0.000 0.604 0.000 0.388 0.008
#&gt; SRR1946690     2  0.1041     0.7998 0.000 0.964 0.000 0.032 0.004
#&gt; SRR1946689     4  0.1671     0.8556 0.000 0.000 0.076 0.924 0.000
#&gt; SRR1946686     1  0.3586     0.6448 0.736 0.000 0.264 0.000 0.000
#&gt; SRR1946685     2  0.1197     0.8057 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1946688     4  0.3966     0.6495 0.000 0.132 0.000 0.796 0.072
#&gt; SRR1946684     5  0.0451     0.8807 0.008 0.000 0.000 0.004 0.988
#&gt; SRR1946683     5  0.1195     0.8708 0.028 0.000 0.012 0.000 0.960
#&gt; SRR1946682     5  0.2563     0.8430 0.000 0.008 0.000 0.120 0.872
#&gt; SRR1946680     4  0.1732     0.8543 0.000 0.000 0.080 0.920 0.000
#&gt; SRR1946681     2  0.4452     0.0824 0.000 0.500 0.496 0.000 0.004
#&gt; SRR1946687     4  0.4014     0.6462 0.016 0.000 0.256 0.728 0.000
#&gt; SRR1946679     2  0.1282     0.8071 0.000 0.952 0.044 0.000 0.004
#&gt; SRR1946678     1  0.1704     0.8920 0.928 0.000 0.004 0.000 0.068
#&gt; SRR1946676     2  0.2536     0.7595 0.000 0.868 0.128 0.000 0.004
#&gt; SRR1946677     5  0.1124     0.8687 0.004 0.000 0.036 0.000 0.960
#&gt; SRR1946672     3  0.1205     0.8276 0.040 0.000 0.956 0.004 0.000
#&gt; SRR1946673     5  0.0451     0.8790 0.008 0.000 0.004 0.000 0.988
#&gt; SRR1946671     2  0.5047     0.1038 0.472 0.496 0.000 0.000 0.032
#&gt; SRR1946669     5  0.0771     0.8777 0.020 0.000 0.004 0.000 0.976
#&gt; SRR1946668     5  0.1943     0.8715 0.020 0.000 0.000 0.056 0.924
#&gt; SRR1946666     1  0.1792     0.8864 0.916 0.000 0.084 0.000 0.000
#&gt; SRR1946667     4  0.1671     0.8556 0.000 0.000 0.076 0.924 0.000
#&gt; SRR1946670     5  0.4768     0.4718 0.000 0.024 0.000 0.384 0.592
#&gt; SRR1946663     5  0.3205     0.8062 0.004 0.004 0.000 0.176 0.816
#&gt; SRR1946664     2  0.0324     0.8096 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1946662     5  0.0566     0.8785 0.012 0.000 0.004 0.000 0.984
#&gt; SRR1946661     5  0.4661     0.7458 0.012 0.156 0.000 0.076 0.756
#&gt; SRR1946660     2  0.5304     0.4505 0.000 0.628 0.000 0.292 0.080
#&gt; SRR1946659     1  0.0609     0.9288 0.980 0.000 0.020 0.000 0.000
#&gt; SRR1946658     5  0.2770     0.8508 0.000 0.044 0.000 0.076 0.880
#&gt; SRR1946657     2  0.0609     0.8118 0.000 0.980 0.020 0.000 0.000
#&gt; SRR1946655     3  0.0451     0.8413 0.000 0.000 0.988 0.008 0.004
#&gt; SRR1946654     3  0.0451     0.8449 0.004 0.008 0.988 0.000 0.000
#&gt; SRR1946653     3  0.6506     0.0463 0.208 0.000 0.468 0.324 0.000
#&gt; SRR1946652     5  0.4495     0.6661 0.000 0.200 0.064 0.000 0.736
#&gt; SRR1946651     2  0.0162     0.8117 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1946650     2  0.0290     0.8108 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1946649     2  0.2522     0.7589 0.108 0.880 0.000 0.000 0.012
#&gt; SRR1946648     3  0.3395     0.6378 0.000 0.000 0.764 0.000 0.236
#&gt; SRR1946647     5  0.0451     0.8797 0.000 0.000 0.004 0.008 0.988
#&gt; SRR1946646     2  0.3477     0.7474 0.112 0.832 0.056 0.000 0.000
#&gt; SRR1946645     1  0.2983     0.8438 0.868 0.004 0.032 0.000 0.096
#&gt; SRR1946644     2  0.0404     0.8123 0.000 0.988 0.012 0.000 0.000
#&gt; SRR1946643     3  0.0771     0.8401 0.000 0.020 0.976 0.004 0.000
#&gt; SRR1946642     1  0.0000     0.9374 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.9374 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0290     0.8442 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1946640     1  0.0000     0.9374 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.9374 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9374 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9374 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.0976    0.85394 0.000 0.000 0.968 0.008 0.008 0.016
#&gt; SRR1946691     2  0.5909    0.00221 0.000 0.420 0.000 0.208 0.000 0.372
#&gt; SRR1946690     2  0.1555    0.75717 0.000 0.940 0.000 0.012 0.040 0.008
#&gt; SRR1946689     4  0.0146    0.78255 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1946686     1  0.3853    0.57815 0.680 0.000 0.304 0.000 0.000 0.016
#&gt; SRR1946685     2  0.1644    0.74186 0.000 0.920 0.004 0.000 0.076 0.000
#&gt; SRR1946688     6  0.6376    0.15742 0.000 0.016 0.000 0.368 0.236 0.380
#&gt; SRR1946684     6  0.3746    0.43765 0.004 0.000 0.012 0.000 0.272 0.712
#&gt; SRR1946683     5  0.1934    0.56138 0.000 0.000 0.044 0.000 0.916 0.040
#&gt; SRR1946682     6  0.4704    0.44147 0.000 0.000 0.000 0.072 0.300 0.628
#&gt; SRR1946680     4  0.0146    0.78255 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1946681     2  0.4877    0.17310 0.000 0.528 0.424 0.000 0.012 0.036
#&gt; SRR1946687     4  0.5283    0.55775 0.196 0.000 0.180 0.620 0.004 0.000
#&gt; SRR1946679     2  0.1655    0.75468 0.000 0.932 0.008 0.000 0.008 0.052
#&gt; SRR1946678     1  0.3927    0.58533 0.712 0.000 0.004 0.000 0.260 0.024
#&gt; SRR1946676     5  0.4798    0.31695 0.000 0.376 0.060 0.000 0.564 0.000
#&gt; SRR1946677     5  0.1572    0.57111 0.000 0.000 0.028 0.000 0.936 0.036
#&gt; SRR1946672     3  0.0727    0.86401 0.004 0.004 0.980 0.004 0.004 0.004
#&gt; SRR1946673     6  0.4381    0.14261 0.000 0.004 0.016 0.000 0.456 0.524
#&gt; SRR1946671     5  0.4357    0.58724 0.108 0.156 0.004 0.000 0.732 0.000
#&gt; SRR1946669     5  0.4576   -0.24784 0.016 0.000 0.012 0.000 0.504 0.468
#&gt; SRR1946668     6  0.1036    0.56606 0.008 0.000 0.004 0.000 0.024 0.964
#&gt; SRR1946666     1  0.2664    0.75189 0.816 0.000 0.184 0.000 0.000 0.000
#&gt; SRR1946667     4  0.0146    0.78255 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1946670     6  0.1542    0.56694 0.000 0.004 0.000 0.052 0.008 0.936
#&gt; SRR1946663     6  0.5255    0.33821 0.000 0.000 0.000 0.096 0.428 0.476
#&gt; SRR1946664     2  0.0603    0.77072 0.000 0.980 0.000 0.004 0.000 0.016
#&gt; SRR1946662     6  0.4297    0.15517 0.004 0.000 0.012 0.000 0.452 0.532
#&gt; SRR1946661     6  0.5011    0.32736 0.000 0.080 0.000 0.000 0.368 0.552
#&gt; SRR1946660     6  0.6947    0.25198 0.000 0.120 0.000 0.128 0.320 0.432
#&gt; SRR1946659     1  0.0508    0.88790 0.984 0.000 0.012 0.004 0.000 0.000
#&gt; SRR1946658     6  0.1788    0.55091 0.000 0.076 0.004 0.000 0.004 0.916
#&gt; SRR1946657     2  0.0260    0.77160 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1946655     3  0.0603    0.85951 0.000 0.000 0.980 0.016 0.004 0.000
#&gt; SRR1946654     3  0.1116    0.85434 0.000 0.004 0.960 0.008 0.028 0.000
#&gt; SRR1946653     4  0.4968    0.32314 0.020 0.000 0.384 0.560 0.036 0.000
#&gt; SRR1946652     5  0.4717    0.55518 0.000 0.124 0.056 0.000 0.740 0.080
#&gt; SRR1946651     2  0.1010    0.76598 0.000 0.960 0.000 0.000 0.036 0.004
#&gt; SRR1946650     2  0.3867   -0.15777 0.000 0.512 0.000 0.000 0.488 0.000
#&gt; SRR1946649     5  0.3606    0.56786 0.016 0.256 0.000 0.000 0.728 0.000
#&gt; SRR1946648     3  0.4095    0.05968 0.000 0.000 0.512 0.000 0.480 0.008
#&gt; SRR1946647     6  0.2531    0.53353 0.000 0.000 0.012 0.000 0.132 0.856
#&gt; SRR1946646     2  0.2467    0.72104 0.088 0.884 0.012 0.000 0.016 0.000
#&gt; SRR1946645     5  0.3000    0.56125 0.156 0.004 0.016 0.000 0.824 0.000
#&gt; SRR1946644     2  0.0363    0.77110 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1946643     3  0.0692    0.86008 0.000 0.020 0.976 0.000 0.004 0.000
#&gt; SRR1946642     1  0.0260    0.89177 0.992 0.000 0.000 0.000 0.008 0.000
#&gt; SRR1946641     1  0.0146    0.89337 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1946656     3  0.0363    0.86437 0.000 0.012 0.988 0.000 0.000 0.000
#&gt; SRR1946640     1  0.0000    0.89437 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000    0.89437 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000    0.89437 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000    0.89437 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.754           0.832       0.919         0.4117 0.604   0.604
#> 3 3 0.624           0.673       0.877         0.4076 0.805   0.689
#> 4 4 0.527           0.677       0.796         0.1754 0.851   0.679
#> 5 5 0.594           0.469       0.721         0.1264 0.828   0.515
#> 6 6 0.678           0.598       0.765         0.0708 0.947   0.761
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.5178      0.884 0.116 0.884
#&gt; SRR1946691     2  0.1184      0.905 0.016 0.984
#&gt; SRR1946690     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946689     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946686     1  0.1414      0.922 0.980 0.020
#&gt; SRR1946685     2  0.1184      0.905 0.016 0.984
#&gt; SRR1946688     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946684     1  0.1184      0.924 0.984 0.016
#&gt; SRR1946683     2  0.9996      0.166 0.488 0.512
#&gt; SRR1946682     2  0.4562      0.897 0.096 0.904
#&gt; SRR1946680     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946681     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946687     2  1.0000      0.122 0.500 0.500
#&gt; SRR1946679     2  0.9323      0.541 0.348 0.652
#&gt; SRR1946678     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946676     2  0.2603      0.904 0.044 0.956
#&gt; SRR1946677     2  0.4562      0.897 0.096 0.904
#&gt; SRR1946672     2  0.5178      0.884 0.116 0.884
#&gt; SRR1946673     2  0.4562      0.897 0.096 0.904
#&gt; SRR1946671     2  0.5059      0.888 0.112 0.888
#&gt; SRR1946669     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946668     1  0.1414      0.922 0.980 0.020
#&gt; SRR1946666     2  1.0000      0.122 0.500 0.500
#&gt; SRR1946667     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946670     2  0.4161      0.900 0.084 0.916
#&gt; SRR1946663     2  0.4562      0.897 0.096 0.904
#&gt; SRR1946664     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946662     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946661     2  0.4690      0.895 0.100 0.900
#&gt; SRR1946660     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946659     1  1.0000     -0.205 0.500 0.500
#&gt; SRR1946658     2  0.0672      0.904 0.008 0.992
#&gt; SRR1946657     2  0.0672      0.904 0.008 0.992
#&gt; SRR1946655     2  0.2603      0.906 0.044 0.956
#&gt; SRR1946654     2  0.1633      0.906 0.024 0.976
#&gt; SRR1946653     2  0.3274      0.905 0.060 0.940
#&gt; SRR1946652     2  0.4562      0.897 0.096 0.904
#&gt; SRR1946651     2  0.4562      0.897 0.096 0.904
#&gt; SRR1946650     2  0.3274      0.905 0.060 0.940
#&gt; SRR1946649     2  0.5059      0.888 0.112 0.888
#&gt; SRR1946648     2  0.4562      0.897 0.096 0.904
#&gt; SRR1946647     1  0.6973      0.708 0.812 0.188
#&gt; SRR1946646     2  0.1184      0.905 0.016 0.984
#&gt; SRR1946645     2  0.4562      0.897 0.096 0.904
#&gt; SRR1946644     2  0.0376      0.902 0.004 0.996
#&gt; SRR1946643     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946642     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946641     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946656     2  0.0000      0.901 0.000 1.000
#&gt; SRR1946640     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946639     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946638     1  0.0000      0.932 1.000 0.000
#&gt; SRR1946637     1  0.0000      0.932 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     2  0.1267     0.7710 0.024 0.972 0.004
#&gt; SRR1946691     2  0.2625     0.7450 0.000 0.916 0.084
#&gt; SRR1946690     3  0.4062     0.7349 0.000 0.164 0.836
#&gt; SRR1946689     3  0.0000     0.7304 0.000 0.000 1.000
#&gt; SRR1946686     1  0.0892     0.9474 0.980 0.020 0.000
#&gt; SRR1946685     2  0.5465     0.4500 0.000 0.712 0.288
#&gt; SRR1946688     3  0.6244     0.3199 0.000 0.440 0.560
#&gt; SRR1946684     1  0.0747     0.9507 0.984 0.016 0.000
#&gt; SRR1946683     2  0.6095     0.3116 0.392 0.608 0.000
#&gt; SRR1946682     2  0.0000     0.7793 0.000 1.000 0.000
#&gt; SRR1946680     3  0.0000     0.7304 0.000 0.000 1.000
#&gt; SRR1946681     2  0.6280    -0.0816 0.000 0.540 0.460
#&gt; SRR1946687     2  0.6140     0.2830 0.404 0.596 0.000
#&gt; SRR1946679     2  0.5138     0.5411 0.252 0.748 0.000
#&gt; SRR1946678     1  0.0000     0.9613 1.000 0.000 0.000
#&gt; SRR1946676     2  0.2998     0.7556 0.016 0.916 0.068
#&gt; SRR1946677     2  0.0000     0.7793 0.000 1.000 0.000
#&gt; SRR1946672     2  0.1267     0.7710 0.024 0.972 0.004
#&gt; SRR1946673     2  0.0000     0.7793 0.000 1.000 0.000
#&gt; SRR1946671     2  0.0747     0.7753 0.016 0.984 0.000
#&gt; SRR1946669     1  0.0000     0.9613 1.000 0.000 0.000
#&gt; SRR1946668     1  0.1163     0.9394 0.972 0.028 0.000
#&gt; SRR1946666     2  0.6140     0.2830 0.404 0.596 0.000
#&gt; SRR1946667     3  0.0000     0.7304 0.000 0.000 1.000
#&gt; SRR1946670     2  0.0592     0.7779 0.000 0.988 0.012
#&gt; SRR1946663     2  0.0000     0.7793 0.000 1.000 0.000
#&gt; SRR1946664     3  0.4062     0.7349 0.000 0.164 0.836
#&gt; SRR1946662     1  0.0000     0.9613 1.000 0.000 0.000
#&gt; SRR1946661     2  0.0237     0.7788 0.004 0.996 0.000
#&gt; SRR1946660     3  0.6244     0.3199 0.000 0.440 0.560
#&gt; SRR1946659     2  0.6140     0.2830 0.404 0.596 0.000
#&gt; SRR1946658     2  0.2796     0.7385 0.000 0.908 0.092
#&gt; SRR1946657     2  0.4235     0.6486 0.000 0.824 0.176
#&gt; SRR1946655     2  0.1860     0.7643 0.000 0.948 0.052
#&gt; SRR1946654     2  0.2356     0.7520 0.000 0.928 0.072
#&gt; SRR1946653     2  0.2339     0.7667 0.012 0.940 0.048
#&gt; SRR1946652     2  0.0000     0.7793 0.000 1.000 0.000
#&gt; SRR1946651     2  0.0000     0.7793 0.000 1.000 0.000
#&gt; SRR1946650     2  0.1411     0.7707 0.000 0.964 0.036
#&gt; SRR1946649     2  0.0747     0.7753 0.016 0.984 0.000
#&gt; SRR1946648     2  0.0000     0.7793 0.000 1.000 0.000
#&gt; SRR1946647     1  0.5397     0.5728 0.720 0.280 0.000
#&gt; SRR1946646     2  0.5465     0.4500 0.000 0.712 0.288
#&gt; SRR1946645     2  0.0000     0.7793 0.000 1.000 0.000
#&gt; SRR1946644     2  0.6140     0.1388 0.000 0.596 0.404
#&gt; SRR1946643     2  0.6280    -0.0816 0.000 0.540 0.460
#&gt; SRR1946642     1  0.0000     0.9613 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.9613 1.000 0.000 0.000
#&gt; SRR1946656     2  0.6280    -0.0816 0.000 0.540 0.460
#&gt; SRR1946640     1  0.0000     0.9613 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.9613 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9613 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9613 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     2  0.3325      0.692 0.024 0.864 0.112 0.000
#&gt; SRR1946691     2  0.4746      0.521 0.000 0.688 0.304 0.008
#&gt; SRR1946690     4  0.5147      0.453 0.000 0.004 0.460 0.536
#&gt; SRR1946689     4  0.0000      0.752 0.000 0.000 0.000 1.000
#&gt; SRR1946686     1  0.0707      0.859 0.980 0.020 0.000 0.000
#&gt; SRR1946685     3  0.4643      0.625 0.000 0.344 0.656 0.000
#&gt; SRR1946688     3  0.6104      0.648 0.000 0.140 0.680 0.180
#&gt; SRR1946684     1  0.0779      0.859 0.980 0.016 0.004 0.000
#&gt; SRR1946683     2  0.5560      0.355 0.392 0.584 0.024 0.000
#&gt; SRR1946682     2  0.2281      0.718 0.000 0.904 0.096 0.000
#&gt; SRR1946680     4  0.0000      0.752 0.000 0.000 0.000 1.000
#&gt; SRR1946681     3  0.5208      0.770 0.000 0.172 0.748 0.080
#&gt; SRR1946687     2  0.5571      0.329 0.396 0.580 0.024 0.000
#&gt; SRR1946679     2  0.5025      0.518 0.252 0.716 0.032 0.000
#&gt; SRR1946678     1  0.3074      0.889 0.848 0.000 0.152 0.000
#&gt; SRR1946676     2  0.4136      0.647 0.016 0.788 0.196 0.000
#&gt; SRR1946677     2  0.1792      0.710 0.000 0.932 0.068 0.000
#&gt; SRR1946672     2  0.3325      0.692 0.024 0.864 0.112 0.000
#&gt; SRR1946673     2  0.1389      0.721 0.000 0.952 0.048 0.000
#&gt; SRR1946671     2  0.2924      0.718 0.016 0.884 0.100 0.000
#&gt; SRR1946669     1  0.0000      0.866 1.000 0.000 0.000 0.000
#&gt; SRR1946668     1  0.1256      0.849 0.964 0.028 0.008 0.000
#&gt; SRR1946666     2  0.5571      0.329 0.396 0.580 0.024 0.000
#&gt; SRR1946667     4  0.0000      0.752 0.000 0.000 0.000 1.000
#&gt; SRR1946670     2  0.2760      0.702 0.000 0.872 0.128 0.000
#&gt; SRR1946663     2  0.2281      0.718 0.000 0.904 0.096 0.000
#&gt; SRR1946664     4  0.5147      0.453 0.000 0.004 0.460 0.536
#&gt; SRR1946662     1  0.0000      0.866 1.000 0.000 0.000 0.000
#&gt; SRR1946661     2  0.1398      0.720 0.004 0.956 0.040 0.000
#&gt; SRR1946660     3  0.6104      0.648 0.000 0.140 0.680 0.180
#&gt; SRR1946659     2  0.5571      0.329 0.396 0.580 0.024 0.000
#&gt; SRR1946658     2  0.5161      0.315 0.000 0.592 0.400 0.008
#&gt; SRR1946657     3  0.4972      0.302 0.000 0.456 0.544 0.000
#&gt; SRR1946655     2  0.4331      0.579 0.000 0.712 0.288 0.000
#&gt; SRR1946654     2  0.4406      0.560 0.000 0.700 0.300 0.000
#&gt; SRR1946653     2  0.4053      0.626 0.004 0.768 0.228 0.000
#&gt; SRR1946652     2  0.2647      0.711 0.000 0.880 0.120 0.000
#&gt; SRR1946651     2  0.2647      0.710 0.000 0.880 0.120 0.000
#&gt; SRR1946650     2  0.3569      0.663 0.000 0.804 0.196 0.000
#&gt; SRR1946649     2  0.2924      0.718 0.016 0.884 0.100 0.000
#&gt; SRR1946648     2  0.1867      0.709 0.000 0.928 0.072 0.000
#&gt; SRR1946647     1  0.4927      0.547 0.712 0.264 0.024 0.000
#&gt; SRR1946646     3  0.4643      0.625 0.000 0.344 0.656 0.000
#&gt; SRR1946645     2  0.1792      0.710 0.000 0.932 0.068 0.000
#&gt; SRR1946644     3  0.4225      0.765 0.000 0.184 0.792 0.024
#&gt; SRR1946643     3  0.5208      0.770 0.000 0.172 0.748 0.080
#&gt; SRR1946642     1  0.3074      0.889 0.848 0.000 0.152 0.000
#&gt; SRR1946641     1  0.3074      0.889 0.848 0.000 0.152 0.000
#&gt; SRR1946656     3  0.5208      0.770 0.000 0.172 0.748 0.080
#&gt; SRR1946640     1  0.3074      0.889 0.848 0.000 0.152 0.000
#&gt; SRR1946639     1  0.3074      0.889 0.848 0.000 0.152 0.000
#&gt; SRR1946638     1  0.3074      0.889 0.848 0.000 0.152 0.000
#&gt; SRR1946637     1  0.3074      0.889 0.848 0.000 0.152 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3   0.556   0.012520 0.000 0.084 0.608 0.004 0.304
#&gt; SRR1946691     3   0.744   0.027515 0.000 0.276 0.424 0.040 0.260
#&gt; SRR1946690     2   0.442   0.000035 0.000 0.552 0.004 0.444 0.000
#&gt; SRR1946689     4   0.104   1.000000 0.000 0.040 0.000 0.960 0.000
#&gt; SRR1946686     1   0.413   0.722033 0.656 0.000 0.340 0.000 0.004
#&gt; SRR1946685     2   0.397   0.576334 0.000 0.752 0.024 0.000 0.224
#&gt; SRR1946688     2   0.189   0.651288 0.000 0.916 0.004 0.080 0.000
#&gt; SRR1946684     1   0.413   0.721857 0.656 0.000 0.340 0.000 0.004
#&gt; SRR1946683     3   0.545   0.152797 0.068 0.000 0.556 0.000 0.376
#&gt; SRR1946682     5   0.331   0.543681 0.000 0.000 0.224 0.000 0.776
#&gt; SRR1946680     4   0.104   1.000000 0.000 0.040 0.000 0.960 0.000
#&gt; SRR1946681     2   0.127   0.692925 0.000 0.960 0.024 0.012 0.004
#&gt; SRR1946687     3   0.449   0.301557 0.080 0.000 0.748 0.000 0.172
#&gt; SRR1946679     3   0.531   0.016884 0.004 0.040 0.584 0.004 0.368
#&gt; SRR1946678     1   0.000   0.822925 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     5   0.391   0.448907 0.000 0.164 0.048 0.000 0.788
#&gt; SRR1946677     5   0.501   0.415393 0.000 0.084 0.232 0.000 0.684
#&gt; SRR1946672     3   0.556   0.012520 0.000 0.084 0.608 0.004 0.304
#&gt; SRR1946673     5   0.517   0.446887 0.000 0.048 0.332 0.004 0.616
#&gt; SRR1946671     5   0.104   0.515407 0.000 0.000 0.040 0.000 0.960
#&gt; SRR1946669     1   0.391   0.735485 0.676 0.000 0.324 0.000 0.000
#&gt; SRR1946668     1   0.420   0.706598 0.640 0.000 0.356 0.000 0.004
#&gt; SRR1946666     3   0.449   0.301557 0.080 0.000 0.748 0.000 0.172
#&gt; SRR1946667     4   0.104   1.000000 0.000 0.040 0.000 0.960 0.000
#&gt; SRR1946670     3   0.636  -0.078050 0.000 0.136 0.504 0.008 0.352
#&gt; SRR1946663     5   0.346   0.544265 0.000 0.004 0.224 0.000 0.772
#&gt; SRR1946664     2   0.442   0.000035 0.000 0.552 0.004 0.444 0.000
#&gt; SRR1946662     1   0.391   0.735485 0.676 0.000 0.324 0.000 0.000
#&gt; SRR1946661     5   0.511   0.440228 0.000 0.040 0.352 0.004 0.604
#&gt; SRR1946660     2   0.189   0.651288 0.000 0.916 0.004 0.080 0.000
#&gt; SRR1946659     3   0.449   0.301557 0.080 0.000 0.748 0.000 0.172
#&gt; SRR1946658     2   0.726  -0.178435 0.000 0.396 0.388 0.040 0.176
#&gt; SRR1946657     2   0.548   0.380169 0.000 0.656 0.172 0.000 0.172
#&gt; SRR1946655     3   0.731   0.039269 0.000 0.236 0.464 0.040 0.260
#&gt; SRR1946654     3   0.700  -0.051680 0.000 0.272 0.388 0.008 0.332
#&gt; SRR1946653     5   0.740   0.049989 0.000 0.208 0.372 0.040 0.380
#&gt; SRR1946652     5   0.448   0.534279 0.000 0.044 0.220 0.004 0.732
#&gt; SRR1946651     5   0.435   0.537921 0.000 0.040 0.212 0.004 0.744
#&gt; SRR1946650     5   0.498   0.514619 0.000 0.088 0.220 0.000 0.692
#&gt; SRR1946649     5   0.104   0.515407 0.000 0.000 0.040 0.000 0.960
#&gt; SRR1946648     5   0.511   0.409097 0.000 0.092 0.232 0.000 0.676
#&gt; SRR1946647     3   0.500  -0.290815 0.388 0.000 0.576 0.000 0.036
#&gt; SRR1946646     2   0.397   0.576334 0.000 0.752 0.024 0.000 0.224
#&gt; SRR1946645     5   0.501   0.415393 0.000 0.084 0.232 0.000 0.684
#&gt; SRR1946644     2   0.201   0.685968 0.000 0.920 0.020 0.000 0.060
#&gt; SRR1946643     2   0.127   0.692925 0.000 0.960 0.024 0.012 0.004
#&gt; SRR1946642     1   0.000   0.822925 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1   0.000   0.822925 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     2   0.127   0.692925 0.000 0.960 0.024 0.012 0.004
#&gt; SRR1946640     1   0.000   0.822925 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1   0.000   0.822925 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1   0.000   0.822925 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1   0.000   0.822925 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.4860      0.499 0.000 0.008 0.516 0.000 0.040 0.436
#&gt; SRR1946691     3  0.2415      0.596 0.000 0.084 0.888 0.000 0.012 0.016
#&gt; SRR1946690     2  0.4372      0.192 0.000 0.544 0.000 0.432 0.000 0.024
#&gt; SRR1946689     4  0.0146      1.000 0.000 0.004 0.000 0.996 0.000 0.000
#&gt; SRR1946686     1  0.3810      0.515 0.572 0.000 0.000 0.000 0.000 0.428
#&gt; SRR1946685     2  0.3659      0.639 0.000 0.752 0.012 0.000 0.224 0.012
#&gt; SRR1946688     2  0.1765      0.737 0.000 0.924 0.000 0.052 0.000 0.024
#&gt; SRR1946684     1  0.3810      0.515 0.572 0.000 0.000 0.000 0.000 0.428
#&gt; SRR1946683     6  0.3050      0.560 0.000 0.000 0.000 0.000 0.236 0.764
#&gt; SRR1946682     5  0.3431      0.618 0.000 0.000 0.228 0.000 0.756 0.016
#&gt; SRR1946680     4  0.0146      1.000 0.000 0.004 0.000 0.996 0.000 0.000
#&gt; SRR1946681     2  0.2045      0.763 0.000 0.920 0.028 0.028 0.024 0.000
#&gt; SRR1946687     6  0.0935      0.675 0.000 0.000 0.004 0.000 0.032 0.964
#&gt; SRR1946679     6  0.6110     -0.128 0.000 0.000 0.268 0.004 0.288 0.440
#&gt; SRR1946678     1  0.0000      0.763 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     5  0.5028      0.471 0.000 0.176 0.004 0.000 0.656 0.164
#&gt; SRR1946677     5  0.5155      0.450 0.000 0.068 0.028 0.000 0.636 0.268
#&gt; SRR1946672     3  0.4860      0.499 0.000 0.008 0.516 0.000 0.040 0.436
#&gt; SRR1946673     5  0.5563      0.563 0.000 0.000 0.332 0.004 0.528 0.136
#&gt; SRR1946671     5  0.2340      0.553 0.000 0.000 0.000 0.000 0.852 0.148
#&gt; SRR1946669     1  0.3774      0.540 0.592 0.000 0.000 0.000 0.000 0.408
#&gt; SRR1946668     1  0.3833      0.488 0.556 0.000 0.000 0.000 0.000 0.444
#&gt; SRR1946666     6  0.0935      0.675 0.000 0.000 0.004 0.000 0.032 0.964
#&gt; SRR1946667     4  0.0146      1.000 0.000 0.004 0.000 0.996 0.000 0.000
#&gt; SRR1946670     3  0.3655      0.497 0.000 0.000 0.800 0.004 0.088 0.108
#&gt; SRR1946663     5  0.3570      0.619 0.000 0.004 0.228 0.000 0.752 0.016
#&gt; SRR1946664     2  0.4372      0.192 0.000 0.544 0.000 0.432 0.000 0.024
#&gt; SRR1946662     1  0.3774      0.540 0.592 0.000 0.000 0.000 0.000 0.408
#&gt; SRR1946661     5  0.5739      0.566 0.000 0.000 0.284 0.004 0.528 0.184
#&gt; SRR1946660     2  0.1765      0.737 0.000 0.924 0.000 0.052 0.000 0.024
#&gt; SRR1946659     6  0.0935      0.675 0.000 0.000 0.004 0.000 0.032 0.964
#&gt; SRR1946658     3  0.3470      0.475 0.000 0.248 0.740 0.000 0.012 0.000
#&gt; SRR1946657     2  0.5254      0.447 0.000 0.668 0.192 0.000 0.104 0.036
#&gt; SRR1946655     3  0.3003      0.636 0.000 0.016 0.812 0.000 0.000 0.172
#&gt; SRR1946654     3  0.6295      0.609 0.000 0.184 0.568 0.000 0.072 0.176
#&gt; SRR1946653     3  0.4552      0.536 0.000 0.012 0.636 0.000 0.032 0.320
#&gt; SRR1946652     5  0.4823      0.602 0.000 0.016 0.316 0.004 0.628 0.036
#&gt; SRR1946651     5  0.4741      0.608 0.000 0.016 0.296 0.004 0.648 0.036
#&gt; SRR1946650     5  0.4358      0.598 0.000 0.100 0.184 0.000 0.716 0.000
#&gt; SRR1946649     5  0.2340      0.553 0.000 0.000 0.000 0.000 0.852 0.148
#&gt; SRR1946648     5  0.5288      0.444 0.000 0.068 0.036 0.000 0.628 0.268
#&gt; SRR1946647     6  0.3428      0.228 0.304 0.000 0.000 0.000 0.000 0.696
#&gt; SRR1946646     2  0.3659      0.639 0.000 0.752 0.012 0.000 0.224 0.012
#&gt; SRR1946645     5  0.5155      0.450 0.000 0.068 0.028 0.000 0.636 0.268
#&gt; SRR1946644     2  0.1779      0.750 0.000 0.920 0.016 0.000 0.064 0.000
#&gt; SRR1946643     2  0.2045      0.763 0.000 0.920 0.028 0.028 0.024 0.000
#&gt; SRR1946642     1  0.0000      0.763 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000      0.763 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     2  0.2045      0.763 0.000 0.920 0.028 0.028 0.024 0.000
#&gt; SRR1946640     1  0.0000      0.763 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.763 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.763 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.763 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.990       0.995         0.4418 0.556   0.556
#> 3 3 0.971           0.949       0.979         0.4043 0.690   0.507
#> 4 4 0.593           0.543       0.742         0.1795 0.812   0.544
#> 5 5 0.599           0.478       0.681         0.0780 0.832   0.465
#> 6 6 0.651           0.405       0.633         0.0505 0.897   0.580
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946691     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946690     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946689     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946686     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946685     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946688     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946684     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946683     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946682     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946680     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946681     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946687     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946679     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946678     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946676     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946677     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946672     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946673     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946671     1  0.7299      0.743 0.796 0.204
#&gt; SRR1946669     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946668     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946666     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946667     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946670     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946663     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946664     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946662     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946661     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946660     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946659     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946658     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946657     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946655     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946654     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946653     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946652     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946651     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946650     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946649     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946648     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946647     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946646     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946645     2  0.0376      0.998 0.004 0.996
#&gt; SRR1946644     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946643     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946642     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946641     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946656     2  0.0000      0.998 0.000 1.000
#&gt; SRR1946640     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946639     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946638     1  0.0000      0.987 1.000 0.000
#&gt; SRR1946637     1  0.0000      0.987 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946691     2   0.355      0.836 0.000 0.868 0.132
#&gt; SRR1946690     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946689     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946686     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946685     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946688     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946684     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946683     2   0.226      0.902 0.068 0.932 0.000
#&gt; SRR1946682     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946680     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946681     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946687     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946679     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946678     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946676     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946677     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946672     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946673     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946671     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946669     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946668     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946666     2   0.571      0.535 0.320 0.680 0.000
#&gt; SRR1946667     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946670     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946663     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946664     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946662     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946661     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946660     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946659     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946658     2   0.626      0.211 0.000 0.552 0.448
#&gt; SRR1946657     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946655     2   0.296      0.871 0.000 0.900 0.100
#&gt; SRR1946654     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946653     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946652     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946651     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946650     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946649     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946648     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946647     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946646     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946645     2   0.000      0.961 0.000 1.000 0.000
#&gt; SRR1946644     3   0.186      0.933 0.000 0.052 0.948
#&gt; SRR1946643     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946642     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946641     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946656     3   0.000      0.993 0.000 0.000 1.000
#&gt; SRR1946640     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946639     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946638     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1946637     1   0.000      1.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3   0.404    0.43058 0.000 0.248 0.752 0.000
#&gt; SRR1946691     2   0.464    0.38277 0.000 0.740 0.240 0.020
#&gt; SRR1946690     4   0.139    0.86938 0.000 0.048 0.000 0.952
#&gt; SRR1946689     4   0.000    0.85957 0.000 0.000 0.000 1.000
#&gt; SRR1946686     1   0.287    0.90859 0.864 0.000 0.136 0.000
#&gt; SRR1946685     2   0.391    0.48331 0.000 0.768 0.232 0.000
#&gt; SRR1946688     4   0.433    0.80712 0.000 0.288 0.000 0.712
#&gt; SRR1946684     1   0.297    0.90503 0.856 0.000 0.144 0.000
#&gt; SRR1946683     3   0.355    0.44774 0.020 0.136 0.844 0.000
#&gt; SRR1946682     2   0.466    0.28058 0.000 0.652 0.348 0.000
#&gt; SRR1946680     4   0.000    0.85957 0.000 0.000 0.000 1.000
#&gt; SRR1946681     4   0.441    0.79733 0.000 0.300 0.000 0.700
#&gt; SRR1946687     3   0.187    0.47857 0.000 0.072 0.928 0.000
#&gt; SRR1946679     3   0.425    0.41918 0.000 0.276 0.724 0.000
#&gt; SRR1946678     1   0.000    0.93602 1.000 0.000 0.000 0.000
#&gt; SRR1946676     2   0.497    0.12061 0.000 0.548 0.452 0.000
#&gt; SRR1946677     3   0.500    0.06846 0.000 0.492 0.508 0.000
#&gt; SRR1946672     3   0.349    0.45812 0.000 0.188 0.812 0.000
#&gt; SRR1946673     3   0.492    0.21413 0.000 0.424 0.576 0.000
#&gt; SRR1946671     3   0.361    0.43870 0.000 0.200 0.800 0.000
#&gt; SRR1946669     1   0.281    0.90989 0.868 0.000 0.132 0.000
#&gt; SRR1946668     1   0.353    0.86644 0.808 0.000 0.192 0.000
#&gt; SRR1946666     3   0.174    0.45190 0.056 0.004 0.940 0.000
#&gt; SRR1946667     4   0.000    0.85957 0.000 0.000 0.000 1.000
#&gt; SRR1946670     3   0.479    0.21103 0.000 0.380 0.620 0.000
#&gt; SRR1946663     2   0.419    0.42293 0.000 0.732 0.268 0.000
#&gt; SRR1946664     4   0.130    0.86904 0.000 0.044 0.000 0.956
#&gt; SRR1946662     1   0.297    0.90503 0.856 0.000 0.144 0.000
#&gt; SRR1946661     3   0.496    0.14144 0.000 0.448 0.552 0.000
#&gt; SRR1946660     4   0.433    0.80712 0.000 0.288 0.000 0.712
#&gt; SRR1946659     3   0.491   -0.21050 0.420 0.000 0.580 0.000
#&gt; SRR1946658     2   0.367    0.45738 0.000 0.852 0.044 0.104
#&gt; SRR1946657     2   0.228    0.53857 0.000 0.904 0.096 0.000
#&gt; SRR1946655     2   0.506    0.25307 0.000 0.648 0.340 0.012
#&gt; SRR1946654     3   0.500   -0.12406 0.000 0.500 0.500 0.000
#&gt; SRR1946653     3   0.480    0.22445 0.000 0.384 0.616 0.000
#&gt; SRR1946652     2   0.471    0.31967 0.000 0.640 0.360 0.000
#&gt; SRR1946651     2   0.452    0.35552 0.000 0.680 0.320 0.000
#&gt; SRR1946650     2   0.281    0.53657 0.000 0.868 0.132 0.000
#&gt; SRR1946649     3   0.498    0.09330 0.000 0.460 0.540 0.000
#&gt; SRR1946648     2   0.498    0.00732 0.000 0.536 0.464 0.000
#&gt; SRR1946647     3   0.130    0.46265 0.000 0.044 0.956 0.000
#&gt; SRR1946646     2   0.365    0.49644 0.000 0.796 0.204 0.000
#&gt; SRR1946645     3   0.500    0.05699 0.000 0.496 0.504 0.000
#&gt; SRR1946644     2   0.401    0.42724 0.000 0.800 0.016 0.184
#&gt; SRR1946643     4   0.353    0.85235 0.000 0.192 0.000 0.808
#&gt; SRR1946642     1   0.000    0.93602 1.000 0.000 0.000 0.000
#&gt; SRR1946641     1   0.000    0.93602 1.000 0.000 0.000 0.000
#&gt; SRR1946656     4   0.413    0.81895 0.000 0.260 0.000 0.740
#&gt; SRR1946640     1   0.000    0.93602 1.000 0.000 0.000 0.000
#&gt; SRR1946639     1   0.000    0.93602 1.000 0.000 0.000 0.000
#&gt; SRR1946638     1   0.000    0.93602 1.000 0.000 0.000 0.000
#&gt; SRR1946637     1   0.000    0.93602 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3   0.613     0.4357 0.000 0.208 0.564 0.000 0.228
#&gt; SRR1946691     2   0.433     0.4024 0.000 0.768 0.092 0.000 0.140
#&gt; SRR1946690     4   0.302     0.7401 0.000 0.132 0.020 0.848 0.000
#&gt; SRR1946689     4   0.000     0.7910 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946686     1   0.418     0.7263 0.668 0.008 0.324 0.000 0.000
#&gt; SRR1946685     5   0.489     0.4432 0.000 0.316 0.044 0.000 0.640
#&gt; SRR1946688     2   0.639     0.0608 0.000 0.484 0.040 0.408 0.068
#&gt; SRR1946684     1   0.420     0.7235 0.664 0.008 0.328 0.000 0.000
#&gt; SRR1946683     3   0.384     0.3838 0.000 0.008 0.732 0.000 0.260
#&gt; SRR1946682     5   0.462     0.4755 0.000 0.224 0.060 0.000 0.716
#&gt; SRR1946680     4   0.000     0.7910 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946681     2   0.438     0.2008 0.000 0.616 0.008 0.376 0.000
#&gt; SRR1946687     3   0.455     0.4899 0.000 0.044 0.704 0.000 0.252
#&gt; SRR1946679     5   0.555    -0.0687 0.000 0.068 0.448 0.000 0.484
#&gt; SRR1946678     1   0.000     0.8330 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     5   0.251     0.5628 0.000 0.028 0.080 0.000 0.892
#&gt; SRR1946677     5   0.433     0.4782 0.000 0.044 0.220 0.000 0.736
#&gt; SRR1946672     3   0.600     0.4386 0.000 0.168 0.576 0.000 0.256
#&gt; SRR1946673     5   0.618     0.1481 0.000 0.168 0.296 0.000 0.536
#&gt; SRR1946671     5   0.431    -0.1323 0.000 0.000 0.492 0.000 0.508
#&gt; SRR1946669     1   0.413     0.7327 0.680 0.008 0.312 0.000 0.000
#&gt; SRR1946668     1   0.453     0.5544 0.544 0.008 0.448 0.000 0.000
#&gt; SRR1946666     3   0.219     0.5528 0.012 0.000 0.904 0.000 0.084
#&gt; SRR1946667     4   0.000     0.7910 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946670     3   0.674     0.2560 0.000 0.288 0.412 0.000 0.300
#&gt; SRR1946663     5   0.500     0.4295 0.000 0.256 0.072 0.000 0.672
#&gt; SRR1946664     4   0.256     0.7565 0.000 0.120 0.008 0.872 0.000
#&gt; SRR1946662     1   0.420     0.7235 0.664 0.008 0.328 0.000 0.000
#&gt; SRR1946661     5   0.301     0.5156 0.000 0.004 0.172 0.000 0.824
#&gt; SRR1946660     2   0.639     0.0608 0.000 0.484 0.040 0.408 0.068
#&gt; SRR1946659     3   0.265     0.4403 0.152 0.000 0.848 0.000 0.000
#&gt; SRR1946658     2   0.236     0.4799 0.000 0.904 0.036 0.000 0.060
#&gt; SRR1946657     5   0.491     0.2101 0.000 0.480 0.024 0.000 0.496
#&gt; SRR1946655     2   0.545     0.2061 0.000 0.636 0.256 0.000 0.108
#&gt; SRR1946654     5   0.663     0.1235 0.000 0.380 0.220 0.000 0.400
#&gt; SRR1946653     3   0.661     0.3154 0.000 0.252 0.460 0.000 0.288
#&gt; SRR1946652     5   0.516     0.4437 0.000 0.256 0.084 0.000 0.660
#&gt; SRR1946651     5   0.367     0.5473 0.000 0.112 0.068 0.000 0.820
#&gt; SRR1946650     5   0.349     0.5234 0.000 0.160 0.028 0.000 0.812
#&gt; SRR1946649     5   0.276     0.5540 0.000 0.024 0.104 0.000 0.872
#&gt; SRR1946648     5   0.619     0.3818 0.000 0.292 0.172 0.000 0.536
#&gt; SRR1946647     3   0.189     0.5584 0.000 0.008 0.920 0.000 0.072
#&gt; SRR1946646     5   0.506     0.3667 0.000 0.384 0.040 0.000 0.576
#&gt; SRR1946645     5   0.459     0.4830 0.000 0.064 0.212 0.000 0.724
#&gt; SRR1946644     2   0.549     0.3061 0.000 0.648 0.032 0.044 0.276
#&gt; SRR1946643     4   0.445    -0.0837 0.000 0.480 0.004 0.516 0.000
#&gt; SRR1946642     1   0.000     0.8330 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1   0.000     0.8330 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     2   0.445     0.1761 0.000 0.592 0.008 0.400 0.000
#&gt; SRR1946640     1   0.000     0.8330 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1   0.000     0.8330 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1   0.000     0.8330 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1   0.000     0.8330 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     5  0.6614    0.35196 0.000 0.108 0.124 0.000 0.520 0.248
#&gt; SRR1946691     6  0.4657   -0.12817 0.000 0.016 0.472 0.000 0.016 0.496
#&gt; SRR1946690     4  0.4364    0.66081 0.000 0.004 0.192 0.732 0.008 0.064
#&gt; SRR1946689     4  0.0000    0.85122 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946686     1  0.5428    0.52243 0.520 0.000 0.024 0.000 0.392 0.064
#&gt; SRR1946685     2  0.4520    0.40926 0.000 0.704 0.224 0.000 0.016 0.056
#&gt; SRR1946688     3  0.6867    0.19513 0.000 0.048 0.448 0.284 0.008 0.212
#&gt; SRR1946684     1  0.5495    0.50140 0.500 0.000 0.024 0.000 0.408 0.068
#&gt; SRR1946683     5  0.3860    0.47694 0.000 0.164 0.000 0.000 0.764 0.072
#&gt; SRR1946682     6  0.5266    0.24114 0.000 0.336 0.100 0.000 0.004 0.560
#&gt; SRR1946680     4  0.0000    0.85122 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946681     3  0.3383    0.44885 0.000 0.000 0.728 0.268 0.000 0.004
#&gt; SRR1946687     5  0.5324    0.51746 0.000 0.184 0.056 0.000 0.672 0.088
#&gt; SRR1946679     5  0.5849    0.25618 0.000 0.384 0.028 0.000 0.488 0.100
#&gt; SRR1946678     1  0.0000    0.78733 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     2  0.3401    0.38377 0.000 0.776 0.004 0.000 0.016 0.204
#&gt; SRR1946677     2  0.3458    0.43518 0.000 0.816 0.044 0.000 0.128 0.012
#&gt; SRR1946672     5  0.6226    0.44689 0.000 0.156 0.088 0.000 0.588 0.168
#&gt; SRR1946673     2  0.6695   -0.01012 0.000 0.380 0.044 0.000 0.208 0.368
#&gt; SRR1946671     5  0.5282    0.17201 0.000 0.416 0.000 0.000 0.484 0.100
#&gt; SRR1946669     1  0.5407    0.53342 0.532 0.000 0.024 0.000 0.380 0.064
#&gt; SRR1946668     5  0.5331   -0.17410 0.316 0.000 0.024 0.000 0.588 0.072
#&gt; SRR1946666     5  0.1760    0.56861 0.004 0.028 0.020 0.000 0.936 0.012
#&gt; SRR1946667     4  0.0000    0.85122 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946670     6  0.6386   -0.05726 0.000 0.104 0.080 0.000 0.308 0.508
#&gt; SRR1946663     6  0.5288    0.23488 0.000 0.344 0.100 0.000 0.004 0.552
#&gt; SRR1946664     4  0.3555    0.75510 0.000 0.004 0.140 0.808 0.008 0.040
#&gt; SRR1946662     1  0.5495    0.50140 0.500 0.000 0.024 0.000 0.408 0.068
#&gt; SRR1946661     2  0.4275    0.36941 0.000 0.728 0.004 0.000 0.076 0.192
#&gt; SRR1946660     3  0.6870    0.18618 0.000 0.048 0.444 0.292 0.008 0.208
#&gt; SRR1946659     5  0.2076    0.55493 0.040 0.004 0.020 0.000 0.920 0.016
#&gt; SRR1946658     3  0.3583    0.26488 0.000 0.008 0.728 0.000 0.004 0.260
#&gt; SRR1946657     2  0.6085    0.16065 0.000 0.444 0.304 0.000 0.004 0.248
#&gt; SRR1946655     3  0.5944    0.08154 0.000 0.036 0.568 0.000 0.140 0.256
#&gt; SRR1946654     2  0.7548   -0.00582 0.000 0.328 0.256 0.000 0.152 0.264
#&gt; SRR1946653     5  0.7174    0.15653 0.000 0.152 0.136 0.000 0.408 0.304
#&gt; SRR1946652     6  0.5451   -0.17772 0.000 0.440 0.068 0.000 0.020 0.472
#&gt; SRR1946651     2  0.4570    0.22877 0.000 0.600 0.016 0.000 0.020 0.364
#&gt; SRR1946650     2  0.4234    0.24896 0.000 0.644 0.032 0.000 0.000 0.324
#&gt; SRR1946649     2  0.3370    0.36943 0.000 0.772 0.004 0.000 0.012 0.212
#&gt; SRR1946648     2  0.6231    0.32573 0.000 0.564 0.244 0.000 0.104 0.088
#&gt; SRR1946647     5  0.0603    0.55931 0.000 0.016 0.000 0.000 0.980 0.004
#&gt; SRR1946646     2  0.5189    0.34252 0.000 0.592 0.324 0.000 0.020 0.064
#&gt; SRR1946645     2  0.3718    0.43423 0.000 0.796 0.068 0.000 0.128 0.008
#&gt; SRR1946644     3  0.5614    0.24020 0.000 0.256 0.600 0.008 0.012 0.124
#&gt; SRR1946643     3  0.3668    0.37982 0.000 0.000 0.668 0.328 0.000 0.004
#&gt; SRR1946642     1  0.0000    0.78733 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0146    0.78735 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR1946656     3  0.3697    0.46321 0.000 0.000 0.732 0.248 0.004 0.016
#&gt; SRR1946640     1  0.0000    0.78733 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0146    0.78735 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0146    0.78735 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0146    0.78735 0.996 0.000 0.004 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.960           0.939       0.976         0.5023 0.499   0.499
#> 3 3 0.715           0.616       0.845         0.2861 0.808   0.630
#> 4 4 0.871           0.860       0.929         0.1250 0.875   0.663
#> 5 5 0.798           0.719       0.865         0.0517 0.946   0.810
#> 6 6 0.761           0.681       0.833         0.0311 0.972   0.885
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.9608      0.372 0.384 0.616
#&gt; SRR1946691     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946690     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946689     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946686     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946685     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946688     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946684     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946683     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946682     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946680     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946681     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946687     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946679     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946678     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946676     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946677     2  0.0376      0.969 0.004 0.996
#&gt; SRR1946672     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946673     1  0.4939      0.864 0.892 0.108
#&gt; SRR1946671     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946669     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946668     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946666     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946667     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946670     2  0.9286      0.467 0.344 0.656
#&gt; SRR1946663     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946664     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946662     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946661     1  0.9491      0.400 0.632 0.368
#&gt; SRR1946660     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946659     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946658     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946657     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946655     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946654     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946653     2  0.2423      0.935 0.040 0.960
#&gt; SRR1946652     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946651     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946650     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946649     1  0.0672      0.970 0.992 0.008
#&gt; SRR1946648     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946647     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946646     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946645     2  0.0376      0.969 0.004 0.996
#&gt; SRR1946644     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946643     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946642     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946641     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946656     2  0.0000      0.972 0.000 1.000
#&gt; SRR1946640     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946639     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946638     1  0.0000      0.977 1.000 0.000
#&gt; SRR1946637     1  0.0000      0.977 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     2  0.8714    0.15024 0.108 0.484 0.408
#&gt; SRR1946691     3  0.2448    0.68144 0.000 0.076 0.924
#&gt; SRR1946690     3  0.0424    0.74674 0.000 0.008 0.992
#&gt; SRR1946689     3  0.0000    0.74690 0.000 0.000 1.000
#&gt; SRR1946686     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946685     3  0.6026    0.23195 0.000 0.376 0.624
#&gt; SRR1946688     3  0.0592    0.74509 0.000 0.012 0.988
#&gt; SRR1946684     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946683     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946682     2  0.6267    0.01872 0.000 0.548 0.452
#&gt; SRR1946680     3  0.0000    0.74690 0.000 0.000 1.000
#&gt; SRR1946681     3  0.0000    0.74690 0.000 0.000 1.000
#&gt; SRR1946687     1  0.1182    0.97423 0.976 0.012 0.012
#&gt; SRR1946679     1  0.0592    0.98682 0.988 0.012 0.000
#&gt; SRR1946678     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946676     3  0.6307    0.00805 0.000 0.488 0.512
#&gt; SRR1946677     2  0.6302   -0.07837 0.000 0.520 0.480
#&gt; SRR1946672     2  0.9144    0.09066 0.408 0.448 0.144
#&gt; SRR1946673     2  0.1163    0.42251 0.028 0.972 0.000
#&gt; SRR1946671     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946669     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946668     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946666     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946667     3  0.0000    0.74690 0.000 0.000 1.000
#&gt; SRR1946670     2  0.8814    0.26369 0.140 0.548 0.312
#&gt; SRR1946663     3  0.6291    0.04322 0.000 0.468 0.532
#&gt; SRR1946664     3  0.0424    0.74674 0.000 0.008 0.992
#&gt; SRR1946662     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946661     2  0.8071    0.17062 0.076 0.564 0.360
#&gt; SRR1946660     3  0.0892    0.74065 0.000 0.020 0.980
#&gt; SRR1946659     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946658     3  0.0892    0.73672 0.000 0.020 0.980
#&gt; SRR1946657     3  0.2066    0.71164 0.000 0.060 0.940
#&gt; SRR1946655     3  0.6295   -0.05104 0.000 0.472 0.528
#&gt; SRR1946654     3  0.6126    0.09028 0.000 0.400 0.600
#&gt; SRR1946653     2  0.6267    0.07088 0.000 0.548 0.452
#&gt; SRR1946652     2  0.1163    0.41323 0.000 0.972 0.028
#&gt; SRR1946651     2  0.6140    0.10402 0.000 0.596 0.404
#&gt; SRR1946650     3  0.6307    0.00380 0.000 0.488 0.512
#&gt; SRR1946649     2  0.6676   -0.01790 0.476 0.516 0.008
#&gt; SRR1946648     3  0.3267    0.63205 0.000 0.116 0.884
#&gt; SRR1946647     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946646     3  0.0237    0.74607 0.000 0.004 0.996
#&gt; SRR1946645     3  0.6274    0.08235 0.000 0.456 0.544
#&gt; SRR1946644     3  0.0424    0.74674 0.000 0.008 0.992
#&gt; SRR1946643     3  0.0000    0.74690 0.000 0.000 1.000
#&gt; SRR1946642     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946656     3  0.0592    0.74093 0.000 0.012 0.988
#&gt; SRR1946640     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000    0.99785 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000    0.99785 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.0336      0.824 0.000 0.008 0.992 0.000
#&gt; SRR1946691     4  0.1833      0.898 0.000 0.032 0.024 0.944
#&gt; SRR1946690     4  0.0000      0.935 0.000 0.000 0.000 1.000
#&gt; SRR1946689     4  0.0000      0.935 0.000 0.000 0.000 1.000
#&gt; SRR1946686     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946685     4  0.4585      0.477 0.000 0.332 0.000 0.668
#&gt; SRR1946688     4  0.0000      0.935 0.000 0.000 0.000 1.000
#&gt; SRR1946684     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946683     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946682     2  0.5355      0.552 0.000 0.620 0.020 0.360
#&gt; SRR1946680     4  0.0000      0.935 0.000 0.000 0.000 1.000
#&gt; SRR1946681     4  0.0000      0.935 0.000 0.000 0.000 1.000
#&gt; SRR1946687     1  0.3975      0.697 0.760 0.000 0.240 0.000
#&gt; SRR1946679     1  0.1677      0.940 0.948 0.040 0.012 0.000
#&gt; SRR1946678     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946676     2  0.2053      0.789 0.000 0.924 0.004 0.072
#&gt; SRR1946677     2  0.2227      0.771 0.000 0.928 0.036 0.036
#&gt; SRR1946672     3  0.2311      0.782 0.076 0.004 0.916 0.004
#&gt; SRR1946673     3  0.4356      0.638 0.000 0.292 0.708 0.000
#&gt; SRR1946671     1  0.0592      0.970 0.984 0.016 0.000 0.000
#&gt; SRR1946669     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946668     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946666     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946667     4  0.0000      0.935 0.000 0.000 0.000 1.000
#&gt; SRR1946670     3  0.2782      0.821 0.004 0.068 0.904 0.024
#&gt; SRR1946663     2  0.5088      0.450 0.000 0.572 0.004 0.424
#&gt; SRR1946664     4  0.0000      0.935 0.000 0.000 0.000 1.000
#&gt; SRR1946662     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946661     2  0.0188      0.759 0.000 0.996 0.004 0.000
#&gt; SRR1946660     4  0.0336      0.931 0.000 0.008 0.000 0.992
#&gt; SRR1946659     1  0.0592      0.970 0.984 0.000 0.016 0.000
#&gt; SRR1946658     4  0.0188      0.933 0.000 0.004 0.000 0.996
#&gt; SRR1946657     4  0.2281      0.859 0.000 0.096 0.000 0.904
#&gt; SRR1946655     3  0.1474      0.821 0.000 0.000 0.948 0.052
#&gt; SRR1946654     3  0.3688      0.667 0.000 0.000 0.792 0.208
#&gt; SRR1946653     3  0.1022      0.828 0.000 0.032 0.968 0.000
#&gt; SRR1946652     3  0.4406      0.638 0.000 0.300 0.700 0.000
#&gt; SRR1946651     2  0.4139      0.739 0.000 0.816 0.040 0.144
#&gt; SRR1946650     2  0.3539      0.757 0.000 0.820 0.004 0.176
#&gt; SRR1946649     2  0.1256      0.754 0.028 0.964 0.008 0.000
#&gt; SRR1946648     4  0.5823      0.620 0.000 0.120 0.176 0.704
#&gt; SRR1946647     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946646     4  0.1807      0.897 0.000 0.052 0.008 0.940
#&gt; SRR1946645     2  0.2797      0.770 0.000 0.900 0.032 0.068
#&gt; SRR1946644     4  0.0188      0.934 0.000 0.000 0.004 0.996
#&gt; SRR1946643     4  0.0188      0.934 0.000 0.000 0.004 0.996
#&gt; SRR1946642     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946656     4  0.1474      0.904 0.000 0.000 0.052 0.948
#&gt; SRR1946640     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.982 1.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.982 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.0727    0.78128 0.000 0.004 0.980 0.012 0.004
#&gt; SRR1946691     2  0.3044    0.76361 0.000 0.840 0.004 0.008 0.148
#&gt; SRR1946690     2  0.0000    0.91344 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946689     2  0.0000    0.91344 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946686     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946685     4  0.3741    0.57788 0.000 0.264 0.000 0.732 0.004
#&gt; SRR1946688     2  0.0162    0.91239 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1946684     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946683     1  0.0162    0.94794 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1946682     5  0.5824    0.36742 0.000 0.248 0.016 0.104 0.632
#&gt; SRR1946680     2  0.0000    0.91344 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946681     2  0.0451    0.91020 0.000 0.988 0.004 0.008 0.000
#&gt; SRR1946687     1  0.5251    0.46868 0.632 0.000 0.308 0.052 0.008
#&gt; SRR1946679     1  0.5184    0.54839 0.668 0.000 0.008 0.260 0.064
#&gt; SRR1946678     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     5  0.4420    0.31564 0.000 0.004 0.000 0.448 0.548
#&gt; SRR1946677     4  0.1331    0.59909 0.000 0.008 0.000 0.952 0.040
#&gt; SRR1946672     3  0.3038    0.71431 0.080 0.000 0.872 0.040 0.008
#&gt; SRR1946673     5  0.5819   -0.13203 0.000 0.000 0.452 0.092 0.456
#&gt; SRR1946671     1  0.2864    0.82912 0.864 0.000 0.000 0.024 0.112
#&gt; SRR1946669     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946668     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946666     1  0.0671    0.93842 0.980 0.000 0.016 0.000 0.004
#&gt; SRR1946667     2  0.0000    0.91344 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946670     3  0.4594    0.37979 0.000 0.008 0.624 0.008 0.360
#&gt; SRR1946663     5  0.6244    0.22886 0.000 0.388 0.004 0.128 0.480
#&gt; SRR1946664     2  0.0000    0.91344 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1946662     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946661     5  0.4182    0.39985 0.000 0.000 0.004 0.352 0.644
#&gt; SRR1946660     2  0.0162    0.91222 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1946659     1  0.0955    0.92991 0.968 0.000 0.028 0.000 0.004
#&gt; SRR1946658     2  0.0992    0.89907 0.000 0.968 0.008 0.000 0.024
#&gt; SRR1946657     2  0.4861    0.62601 0.000 0.732 0.012 0.072 0.184
#&gt; SRR1946655     3  0.1205    0.77965 0.000 0.040 0.956 0.004 0.000
#&gt; SRR1946654     3  0.3659    0.57362 0.000 0.220 0.768 0.012 0.000
#&gt; SRR1946653     3  0.0865    0.77561 0.000 0.004 0.972 0.000 0.024
#&gt; SRR1946652     5  0.5157   -0.06475 0.000 0.000 0.440 0.040 0.520
#&gt; SRR1946651     5  0.2802    0.48252 0.000 0.008 0.016 0.100 0.876
#&gt; SRR1946650     5  0.5754    0.42589 0.000 0.136 0.000 0.260 0.604
#&gt; SRR1946649     5  0.4060    0.41334 0.000 0.000 0.000 0.360 0.640
#&gt; SRR1946648     4  0.5450    0.56532 0.000 0.228 0.124 0.648 0.000
#&gt; SRR1946647     1  0.0162    0.94813 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946646     2  0.4670   -0.00303 0.000 0.548 0.004 0.440 0.008
#&gt; SRR1946645     4  0.1012    0.61569 0.000 0.012 0.000 0.968 0.020
#&gt; SRR1946644     2  0.0510    0.90862 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1946643     2  0.0566    0.90848 0.000 0.984 0.004 0.012 0.000
#&gt; SRR1946642     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     2  0.1809    0.86654 0.000 0.928 0.060 0.012 0.000
#&gt; SRR1946640     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000    0.94998 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.0862    0.76605 0.000 0.008 0.972 0.000 0.004 0.016
#&gt; SRR1946691     4  0.3673    0.64186 0.000 0.024 0.008 0.764 0.000 0.204
#&gt; SRR1946690     4  0.0260    0.90826 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1946689     4  0.0000    0.90868 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946686     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946685     5  0.3393    0.58715 0.000 0.020 0.000 0.192 0.784 0.004
#&gt; SRR1946688     4  0.0717    0.90388 0.000 0.000 0.000 0.976 0.008 0.016
#&gt; SRR1946684     1  0.0146    0.90718 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1946683     1  0.0891    0.89753 0.968 0.000 0.000 0.000 0.008 0.024
#&gt; SRR1946682     6  0.5702    0.37028 0.000 0.156 0.012 0.124 0.048 0.660
#&gt; SRR1946680     4  0.0000    0.90868 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946681     4  0.1313    0.89328 0.000 0.000 0.004 0.952 0.016 0.028
#&gt; SRR1946687     1  0.6433    0.31505 0.524 0.008 0.292 0.000 0.056 0.120
#&gt; SRR1946679     1  0.7343    0.26546 0.496 0.120 0.028 0.000 0.192 0.164
#&gt; SRR1946678     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     2  0.5776    0.41594 0.000 0.536 0.000 0.012 0.300 0.152
#&gt; SRR1946677     5  0.2750    0.45688 0.000 0.048 0.004 0.000 0.868 0.080
#&gt; SRR1946672     3  0.3551    0.68310 0.060 0.008 0.828 0.000 0.012 0.092
#&gt; SRR1946673     2  0.6310    0.09347 0.000 0.496 0.296 0.000 0.036 0.172
#&gt; SRR1946671     1  0.4669    0.64514 0.728 0.160 0.000 0.000 0.032 0.080
#&gt; SRR1946669     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946668     1  0.0777    0.89837 0.972 0.004 0.000 0.000 0.000 0.024
#&gt; SRR1946666     1  0.2786    0.84068 0.876 0.008 0.060 0.000 0.004 0.052
#&gt; SRR1946667     4  0.0000    0.90868 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946670     6  0.5915    0.00947 0.000 0.212 0.360 0.000 0.000 0.428
#&gt; SRR1946663     6  0.6077    0.36370 0.000 0.124 0.000 0.252 0.056 0.568
#&gt; SRR1946664     4  0.0260    0.90826 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1946662     1  0.0291    0.90618 0.992 0.004 0.000 0.000 0.000 0.004
#&gt; SRR1946661     2  0.5575    0.31397 0.000 0.532 0.000 0.000 0.172 0.296
#&gt; SRR1946660     4  0.0725    0.90418 0.000 0.000 0.000 0.976 0.012 0.012
#&gt; SRR1946659     1  0.2895    0.83408 0.868 0.008 0.072 0.000 0.004 0.048
#&gt; SRR1946658     4  0.1364    0.89308 0.000 0.004 0.004 0.944 0.000 0.048
#&gt; SRR1946657     4  0.5757    0.46648 0.000 0.236 0.004 0.620 0.072 0.068
#&gt; SRR1946655     3  0.2203    0.75578 0.000 0.004 0.896 0.084 0.000 0.016
#&gt; SRR1946654     3  0.4397    0.54792 0.000 0.012 0.724 0.220 0.024 0.020
#&gt; SRR1946653     3  0.1480    0.75227 0.000 0.040 0.940 0.000 0.000 0.020
#&gt; SRR1946652     2  0.5057    0.17764 0.000 0.612 0.288 0.000 0.004 0.096
#&gt; SRR1946651     2  0.2371    0.39212 0.000 0.900 0.000 0.016 0.032 0.052
#&gt; SRR1946650     2  0.6377    0.35821 0.000 0.576 0.000 0.116 0.140 0.168
#&gt; SRR1946649     2  0.5145    0.45190 0.000 0.624 0.000 0.000 0.200 0.176
#&gt; SRR1946648     5  0.4826    0.55521 0.000 0.004 0.100 0.152 0.720 0.024
#&gt; SRR1946647     1  0.2730    0.84303 0.872 0.012 0.012 0.000 0.008 0.096
#&gt; SRR1946646     5  0.4827    0.15624 0.000 0.008 0.004 0.464 0.496 0.028
#&gt; SRR1946645     5  0.1334    0.51002 0.000 0.032 0.000 0.000 0.948 0.020
#&gt; SRR1946644     4  0.2182    0.86341 0.000 0.008 0.000 0.904 0.068 0.020
#&gt; SRR1946643     4  0.1313    0.89328 0.000 0.000 0.004 0.952 0.016 0.028
#&gt; SRR1946642     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     4  0.2703    0.83243 0.000 0.000 0.080 0.876 0.016 0.028
#&gt; SRR1946640     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000    0.90824 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.952       0.980         0.3688 0.623   0.623
#> 3 3 0.831           0.852       0.947         0.4405 0.752   0.629
#> 4 4 0.609           0.598       0.838         0.2462 0.793   0.577
#> 5 5 0.737           0.724       0.881         0.1197 0.901   0.695
#> 6 6 0.692           0.722       0.848         0.0564 0.959   0.837
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2   0.000      0.991 0.000 1.000
#&gt; SRR1946691     2   0.000      0.991 0.000 1.000
#&gt; SRR1946690     2   0.000      0.991 0.000 1.000
#&gt; SRR1946689     2   0.000      0.991 0.000 1.000
#&gt; SRR1946686     1   0.000      0.938 1.000 0.000
#&gt; SRR1946685     2   0.000      0.991 0.000 1.000
#&gt; SRR1946688     2   0.000      0.991 0.000 1.000
#&gt; SRR1946684     1   0.000      0.938 1.000 0.000
#&gt; SRR1946683     2   0.184      0.963 0.028 0.972
#&gt; SRR1946682     2   0.000      0.991 0.000 1.000
#&gt; SRR1946680     2   0.000      0.991 0.000 1.000
#&gt; SRR1946681     2   0.000      0.991 0.000 1.000
#&gt; SRR1946687     2   0.000      0.991 0.000 1.000
#&gt; SRR1946679     2   0.000      0.991 0.000 1.000
#&gt; SRR1946678     1   0.000      0.938 1.000 0.000
#&gt; SRR1946676     2   0.000      0.991 0.000 1.000
#&gt; SRR1946677     2   0.000      0.991 0.000 1.000
#&gt; SRR1946672     2   0.000      0.991 0.000 1.000
#&gt; SRR1946673     2   0.000      0.991 0.000 1.000
#&gt; SRR1946671     2   0.000      0.991 0.000 1.000
#&gt; SRR1946669     1   0.000      0.938 1.000 0.000
#&gt; SRR1946668     1   0.943      0.471 0.640 0.360
#&gt; SRR1946666     2   0.844      0.593 0.272 0.728
#&gt; SRR1946667     2   0.000      0.991 0.000 1.000
#&gt; SRR1946670     2   0.000      0.991 0.000 1.000
#&gt; SRR1946663     2   0.000      0.991 0.000 1.000
#&gt; SRR1946664     2   0.000      0.991 0.000 1.000
#&gt; SRR1946662     1   0.000      0.938 1.000 0.000
#&gt; SRR1946661     2   0.000      0.991 0.000 1.000
#&gt; SRR1946660     2   0.000      0.991 0.000 1.000
#&gt; SRR1946659     1   0.943      0.471 0.640 0.360
#&gt; SRR1946658     2   0.000      0.991 0.000 1.000
#&gt; SRR1946657     2   0.000      0.991 0.000 1.000
#&gt; SRR1946655     2   0.000      0.991 0.000 1.000
#&gt; SRR1946654     2   0.000      0.991 0.000 1.000
#&gt; SRR1946653     2   0.000      0.991 0.000 1.000
#&gt; SRR1946652     2   0.000      0.991 0.000 1.000
#&gt; SRR1946651     2   0.000      0.991 0.000 1.000
#&gt; SRR1946650     2   0.000      0.991 0.000 1.000
#&gt; SRR1946649     2   0.000      0.991 0.000 1.000
#&gt; SRR1946648     2   0.000      0.991 0.000 1.000
#&gt; SRR1946647     2   0.163      0.967 0.024 0.976
#&gt; SRR1946646     2   0.000      0.991 0.000 1.000
#&gt; SRR1946645     2   0.000      0.991 0.000 1.000
#&gt; SRR1946644     2   0.000      0.991 0.000 1.000
#&gt; SRR1946643     2   0.000      0.991 0.000 1.000
#&gt; SRR1946642     1   0.000      0.938 1.000 0.000
#&gt; SRR1946641     1   0.000      0.938 1.000 0.000
#&gt; SRR1946656     2   0.000      0.991 0.000 1.000
#&gt; SRR1946640     1   0.000      0.938 1.000 0.000
#&gt; SRR1946639     1   0.000      0.938 1.000 0.000
#&gt; SRR1946638     1   0.000      0.938 1.000 0.000
#&gt; SRR1946637     1   0.000      0.938 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946691     2  0.3192     0.8191 0.000 0.888 0.112
#&gt; SRR1946690     3  0.0000     0.7221 0.000 0.000 1.000
#&gt; SRR1946689     3  0.0000     0.7221 0.000 0.000 1.000
#&gt; SRR1946686     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946685     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946688     3  0.6140     0.4328 0.000 0.404 0.596
#&gt; SRR1946684     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946683     2  0.0237     0.9389 0.004 0.996 0.000
#&gt; SRR1946682     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946680     3  0.0000     0.7221 0.000 0.000 1.000
#&gt; SRR1946681     2  0.6192     0.0915 0.000 0.580 0.420
#&gt; SRR1946687     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946679     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946678     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946676     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946677     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946672     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946673     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946671     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946669     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946668     2  0.0424     0.9358 0.008 0.992 0.000
#&gt; SRR1946666     2  0.0237     0.9389 0.004 0.996 0.000
#&gt; SRR1946667     3  0.0000     0.7221 0.000 0.000 1.000
#&gt; SRR1946670     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946663     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946664     3  0.0000     0.7221 0.000 0.000 1.000
#&gt; SRR1946662     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946661     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946660     3  0.6215     0.3842 0.000 0.428 0.572
#&gt; SRR1946659     2  0.0237     0.9389 0.004 0.996 0.000
#&gt; SRR1946658     2  0.1643     0.8995 0.000 0.956 0.044
#&gt; SRR1946657     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946655     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946654     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946653     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946652     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946651     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946650     2  0.4346     0.7122 0.000 0.816 0.184
#&gt; SRR1946649     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946648     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946647     2  0.0237     0.9389 0.004 0.996 0.000
#&gt; SRR1946646     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946645     2  0.0000     0.9418 0.000 1.000 0.000
#&gt; SRR1946644     2  0.6192     0.0915 0.000 0.580 0.420
#&gt; SRR1946643     3  0.6215     0.3842 0.000 0.428 0.572
#&gt; SRR1946642     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946656     2  0.5760     0.3896 0.000 0.672 0.328
#&gt; SRR1946640     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     1.0000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.0921     0.6935 0.000 0.028 0.972 0.000
#&gt; SRR1946691     3  0.4843     0.0876 0.000 0.396 0.604 0.000
#&gt; SRR1946690     4  0.4999     0.5968 0.000 0.492 0.000 0.508
#&gt; SRR1946689     4  0.0000     0.8744 0.000 0.000 0.000 1.000
#&gt; SRR1946686     1  0.0188     0.9905 0.996 0.000 0.004 0.000
#&gt; SRR1946685     3  0.4730     0.1845 0.000 0.364 0.636 0.000
#&gt; SRR1946688     2  0.0000     0.4530 0.000 1.000 0.000 0.000
#&gt; SRR1946684     1  0.0921     0.9707 0.972 0.000 0.028 0.000
#&gt; SRR1946683     3  0.0000     0.6992 0.000 0.000 1.000 0.000
#&gt; SRR1946682     3  0.4406     0.3141 0.000 0.300 0.700 0.000
#&gt; SRR1946680     4  0.0000     0.8744 0.000 0.000 0.000 1.000
#&gt; SRR1946681     2  0.4933     0.3174 0.000 0.568 0.432 0.000
#&gt; SRR1946687     3  0.0000     0.6992 0.000 0.000 1.000 0.000
#&gt; SRR1946679     3  0.0000     0.6992 0.000 0.000 1.000 0.000
#&gt; SRR1946678     1  0.0000     0.9930 1.000 0.000 0.000 0.000
#&gt; SRR1946676     2  0.4522     0.5960 0.000 0.680 0.320 0.000
#&gt; SRR1946677     3  0.4746     0.1481 0.000 0.368 0.632 0.000
#&gt; SRR1946672     3  0.0000     0.6992 0.000 0.000 1.000 0.000
#&gt; SRR1946673     3  0.0921     0.6935 0.000 0.028 0.972 0.000
#&gt; SRR1946671     3  0.0188     0.6974 0.000 0.004 0.996 0.000
#&gt; SRR1946669     1  0.0000     0.9930 1.000 0.000 0.000 0.000
#&gt; SRR1946668     3  0.0188     0.6975 0.004 0.000 0.996 0.000
#&gt; SRR1946666     3  0.0000     0.6992 0.000 0.000 1.000 0.000
#&gt; SRR1946667     4  0.0000     0.8744 0.000 0.000 0.000 1.000
#&gt; SRR1946670     3  0.1022     0.6919 0.000 0.032 0.968 0.000
#&gt; SRR1946663     2  0.3024     0.5703 0.000 0.852 0.148 0.000
#&gt; SRR1946664     4  0.3311     0.8302 0.000 0.172 0.000 0.828
#&gt; SRR1946662     1  0.0921     0.9707 0.972 0.000 0.028 0.000
#&gt; SRR1946661     3  0.0707     0.6958 0.000 0.020 0.980 0.000
#&gt; SRR1946660     2  0.0000     0.4530 0.000 1.000 0.000 0.000
#&gt; SRR1946659     3  0.0000     0.6992 0.000 0.000 1.000 0.000
#&gt; SRR1946658     3  0.4907     0.0208 0.000 0.420 0.580 0.000
#&gt; SRR1946657     3  0.4907     0.0208 0.000 0.420 0.580 0.000
#&gt; SRR1946655     3  0.4888     0.0460 0.000 0.412 0.588 0.000
#&gt; SRR1946654     3  0.4907     0.0208 0.000 0.420 0.580 0.000
#&gt; SRR1946653     3  0.4907     0.0208 0.000 0.420 0.580 0.000
#&gt; SRR1946652     2  0.4522     0.5960 0.000 0.680 0.320 0.000
#&gt; SRR1946651     2  0.4522     0.5960 0.000 0.680 0.320 0.000
#&gt; SRR1946650     2  0.4522     0.5960 0.000 0.680 0.320 0.000
#&gt; SRR1946649     2  0.4522     0.5960 0.000 0.680 0.320 0.000
#&gt; SRR1946648     3  0.1118     0.6893 0.000 0.036 0.964 0.000
#&gt; SRR1946647     3  0.0000     0.6992 0.000 0.000 1.000 0.000
#&gt; SRR1946646     3  0.4877     0.0572 0.000 0.408 0.592 0.000
#&gt; SRR1946645     2  0.4999     0.2132 0.000 0.508 0.492 0.000
#&gt; SRR1946644     2  0.3873     0.4512 0.000 0.772 0.228 0.000
#&gt; SRR1946643     2  0.4933     0.3174 0.000 0.568 0.432 0.000
#&gt; SRR1946642     1  0.0000     0.9930 1.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.9930 1.000 0.000 0.000 0.000
#&gt; SRR1946656     2  0.4933     0.3174 0.000 0.568 0.432 0.000
#&gt; SRR1946640     1  0.0000     0.9930 1.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.9930 1.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9930 1.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9930 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.0404     0.8429 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1946691     3  0.3274     0.6924 0.000 0.000 0.780 0.000 0.220
#&gt; SRR1946690     2  0.4109    -0.2178 0.000 0.700 0.000 0.288 0.012
#&gt; SRR1946689     4  0.0000     0.8747 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946686     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946685     5  0.3636     0.4815 0.000 0.000 0.272 0.000 0.728
#&gt; SRR1946688     2  0.3932     0.1736 0.000 0.672 0.000 0.000 0.328
#&gt; SRR1946684     1  0.0404     0.9871 0.988 0.000 0.012 0.000 0.000
#&gt; SRR1946683     3  0.0000     0.8437 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946682     5  0.3816     0.5617 0.000 0.000 0.304 0.000 0.696
#&gt; SRR1946680     4  0.0000     0.8747 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946681     2  0.4150     0.3810 0.000 0.612 0.388 0.000 0.000
#&gt; SRR1946687     3  0.0000     0.8437 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946679     3  0.0000     0.8437 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946678     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     5  0.0404     0.8243 0.000 0.000 0.012 0.000 0.988
#&gt; SRR1946677     5  0.3242     0.6592 0.000 0.000 0.216 0.000 0.784
#&gt; SRR1946672     3  0.0000     0.8437 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946673     3  0.0404     0.8429 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1946671     3  0.0404     0.8381 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1946669     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946668     3  0.0162     0.8423 0.004 0.000 0.996 0.000 0.000
#&gt; SRR1946666     3  0.0000     0.8437 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946667     4  0.0000     0.8747 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946670     3  0.0510     0.8421 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1946663     5  0.0162     0.8129 0.000 0.004 0.000 0.000 0.996
#&gt; SRR1946664     4  0.4150     0.5499 0.000 0.388 0.000 0.612 0.000
#&gt; SRR1946662     1  0.0404     0.9871 0.988 0.000 0.012 0.000 0.000
#&gt; SRR1946661     3  0.0963     0.8249 0.000 0.000 0.964 0.000 0.036
#&gt; SRR1946660     2  0.3949     0.1632 0.000 0.668 0.000 0.000 0.332
#&gt; SRR1946659     3  0.0000     0.8437 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946658     3  0.6511     0.0146 0.000 0.336 0.460 0.000 0.204
#&gt; SRR1946657     3  0.3274     0.6924 0.000 0.000 0.780 0.000 0.220
#&gt; SRR1946655     3  0.6503     0.0288 0.000 0.332 0.464 0.000 0.204
#&gt; SRR1946654     3  0.3508     0.6546 0.000 0.000 0.748 0.000 0.252
#&gt; SRR1946653     3  0.3274     0.6924 0.000 0.000 0.780 0.000 0.220
#&gt; SRR1946652     5  0.0404     0.8243 0.000 0.000 0.012 0.000 0.988
#&gt; SRR1946651     5  0.0404     0.8243 0.000 0.000 0.012 0.000 0.988
#&gt; SRR1946650     5  0.0000     0.8143 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1946649     5  0.0404     0.8243 0.000 0.000 0.012 0.000 0.988
#&gt; SRR1946648     3  0.0404     0.8429 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1946647     3  0.0000     0.8437 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946646     3  0.3305     0.6890 0.000 0.000 0.776 0.000 0.224
#&gt; SRR1946645     5  0.2929     0.7029 0.000 0.000 0.180 0.000 0.820
#&gt; SRR1946644     2  0.5927     0.3903 0.000 0.592 0.172 0.000 0.236
#&gt; SRR1946643     2  0.4150     0.3810 0.000 0.612 0.388 0.000 0.000
#&gt; SRR1946642     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     2  0.4150     0.3810 0.000 0.612 0.388 0.000 0.000
#&gt; SRR1946640     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     0.9972 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     5  0.0713      0.827 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1946691     5  0.3357      0.687 0.000 0.224 0.004 0.000 0.764 0.008
#&gt; SRR1946690     6  0.5313      0.591 0.000 0.000 0.324 0.124 0.000 0.552
#&gt; SRR1946689     4  0.0000      0.787 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946686     1  0.3360      0.782 0.732 0.000 0.000 0.000 0.004 0.264
#&gt; SRR1946685     2  0.3126      0.543 0.000 0.752 0.000 0.000 0.248 0.000
#&gt; SRR1946688     6  0.4109      0.694 0.000 0.012 0.412 0.000 0.000 0.576
#&gt; SRR1946684     1  0.0713      0.603 0.972 0.000 0.000 0.000 0.028 0.000
#&gt; SRR1946683     5  0.3151      0.640 0.252 0.000 0.000 0.000 0.748 0.000
#&gt; SRR1946682     2  0.4375      0.613 0.016 0.680 0.000 0.000 0.276 0.028
#&gt; SRR1946680     4  0.0000      0.787 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946681     3  0.2793      0.805 0.000 0.000 0.800 0.000 0.200 0.000
#&gt; SRR1946687     5  0.0146      0.826 0.004 0.000 0.000 0.000 0.996 0.000
#&gt; SRR1946679     5  0.0000      0.826 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946678     1  0.3804      0.851 0.576 0.000 0.000 0.000 0.000 0.424
#&gt; SRR1946676     2  0.0000      0.820 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946677     2  0.2793      0.687 0.000 0.800 0.000 0.000 0.200 0.000
#&gt; SRR1946672     5  0.0000      0.826 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1946673     5  0.0713      0.827 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1946671     5  0.0692      0.824 0.004 0.020 0.000 0.000 0.976 0.000
#&gt; SRR1946669     1  0.0146      0.629 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1946668     5  0.3804      0.420 0.424 0.000 0.000 0.000 0.576 0.000
#&gt; SRR1946666     5  0.0260      0.826 0.008 0.000 0.000 0.000 0.992 0.000
#&gt; SRR1946667     4  0.0000      0.787 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1946670     5  0.0790      0.827 0.000 0.032 0.000 0.000 0.968 0.000
#&gt; SRR1946663     2  0.2933      0.638 0.000 0.796 0.004 0.000 0.000 0.200
#&gt; SRR1946664     4  0.5880     -0.200 0.000 0.000 0.200 0.424 0.000 0.376
#&gt; SRR1946662     1  0.0713      0.603 0.972 0.000 0.000 0.000 0.028 0.000
#&gt; SRR1946661     5  0.1075      0.818 0.000 0.048 0.000 0.000 0.952 0.000
#&gt; SRR1946660     6  0.3804      0.689 0.000 0.000 0.424 0.000 0.000 0.576
#&gt; SRR1946659     5  0.0260      0.826 0.008 0.000 0.000 0.000 0.992 0.000
#&gt; SRR1946658     3  0.5370      0.728 0.000 0.192 0.588 0.000 0.220 0.000
#&gt; SRR1946657     5  0.3050      0.691 0.000 0.236 0.000 0.000 0.764 0.000
#&gt; SRR1946655     3  0.5392      0.725 0.000 0.192 0.584 0.000 0.224 0.000
#&gt; SRR1946654     5  0.3175      0.663 0.000 0.256 0.000 0.000 0.744 0.000
#&gt; SRR1946653     5  0.2941      0.699 0.000 0.220 0.000 0.000 0.780 0.000
#&gt; SRR1946652     2  0.0260      0.817 0.000 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1946651     2  0.0000      0.820 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946650     2  0.0000      0.820 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946649     2  0.0000      0.820 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946648     5  0.0713      0.827 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1946647     5  0.2912      0.621 0.216 0.000 0.000 0.000 0.784 0.000
#&gt; SRR1946646     5  0.3050      0.691 0.000 0.236 0.000 0.000 0.764 0.000
#&gt; SRR1946645     2  0.2454      0.729 0.000 0.840 0.000 0.000 0.160 0.000
#&gt; SRR1946644     6  0.6578      0.175 0.000 0.224 0.080 0.000 0.172 0.524
#&gt; SRR1946643     3  0.2793      0.805 0.000 0.000 0.800 0.000 0.200 0.000
#&gt; SRR1946642     1  0.3804      0.851 0.576 0.000 0.000 0.000 0.000 0.424
#&gt; SRR1946641     1  0.3804      0.851 0.576 0.000 0.000 0.000 0.000 0.424
#&gt; SRR1946656     3  0.2793      0.805 0.000 0.000 0.800 0.000 0.200 0.000
#&gt; SRR1946640     1  0.3804      0.851 0.576 0.000 0.000 0.000 0.000 0.424
#&gt; SRR1946639     1  0.3804      0.851 0.576 0.000 0.000 0.000 0.000 0.424
#&gt; SRR1946638     1  0.3804      0.851 0.576 0.000 0.000 0.000 0.000 0.424
#&gt; SRR1946637     1  0.3804      0.851 0.576 0.000 0.000 0.000 0.000 0.424
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.463           0.793       0.862         0.3241 0.766   0.766
#> 3 3 0.310           0.518       0.701         0.7411 0.623   0.508
#> 4 4 0.423           0.470       0.713         0.1783 0.680   0.436
#> 5 5 0.384           0.397       0.617         0.1172 0.623   0.251
#> 6 6 0.552           0.461       0.720         0.0999 0.856   0.442
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946691     2  0.4431      0.820 0.092 0.908
#&gt; SRR1946690     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946689     2  0.9358      0.631 0.352 0.648
#&gt; SRR1946686     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946685     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946688     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946684     2  0.3733      0.822 0.072 0.928
#&gt; SRR1946683     2  0.2043      0.831 0.032 0.968
#&gt; SRR1946682     2  0.2948      0.819 0.052 0.948
#&gt; SRR1946680     2  0.9129      0.655 0.328 0.672
#&gt; SRR1946681     2  0.3274      0.829 0.060 0.940
#&gt; SRR1946687     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946679     2  0.2423      0.830 0.040 0.960
#&gt; SRR1946678     1  0.5294      0.965 0.880 0.120
#&gt; SRR1946676     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946677     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946672     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946673     2  0.3584      0.821 0.068 0.932
#&gt; SRR1946671     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946669     2  0.6247      0.726 0.156 0.844
#&gt; SRR1946668     2  0.4022      0.822 0.080 0.920
#&gt; SRR1946666     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946667     2  0.9358      0.631 0.352 0.648
#&gt; SRR1946670     2  0.4298      0.821 0.088 0.912
#&gt; SRR1946663     2  0.2043      0.819 0.032 0.968
#&gt; SRR1946664     2  0.0938      0.827 0.012 0.988
#&gt; SRR1946662     2  0.2948      0.828 0.052 0.948
#&gt; SRR1946661     2  0.1414      0.824 0.020 0.980
#&gt; SRR1946660     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946659     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946658     2  0.4298      0.821 0.088 0.912
#&gt; SRR1946657     2  0.0672      0.831 0.008 0.992
#&gt; SRR1946655     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946654     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946653     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946652     2  0.3584      0.821 0.068 0.932
#&gt; SRR1946651     2  0.2603      0.811 0.044 0.956
#&gt; SRR1946650     2  0.1414      0.824 0.020 0.980
#&gt; SRR1946649     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946648     2  0.8763      0.679 0.296 0.704
#&gt; SRR1946647     2  0.4298      0.822 0.088 0.912
#&gt; SRR1946646     2  0.8327      0.699 0.264 0.736
#&gt; SRR1946645     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946644     2  0.0938      0.832 0.012 0.988
#&gt; SRR1946643     2  0.9087      0.658 0.324 0.676
#&gt; SRR1946642     1  0.5178      0.970 0.884 0.116
#&gt; SRR1946641     1  0.4562      0.984 0.904 0.096
#&gt; SRR1946656     2  0.9209      0.656 0.336 0.664
#&gt; SRR1946640     1  0.4562      0.984 0.904 0.096
#&gt; SRR1946639     1  0.4562      0.984 0.904 0.096
#&gt; SRR1946638     1  0.4298      0.979 0.912 0.088
#&gt; SRR1946637     1  0.4022      0.971 0.920 0.080
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.5873     0.5765 0.004 0.312 0.684
#&gt; SRR1946691     3  0.6192     0.2578 0.000 0.420 0.580
#&gt; SRR1946690     2  0.2486     0.6715 0.008 0.932 0.060
#&gt; SRR1946689     3  0.6410     0.4988 0.004 0.420 0.576
#&gt; SRR1946686     3  0.8896     0.4255 0.264 0.172 0.564
#&gt; SRR1946685     2  0.1337     0.6945 0.016 0.972 0.012
#&gt; SRR1946688     2  0.2280     0.6755 0.008 0.940 0.052
#&gt; SRR1946684     3  0.7874     0.0581 0.064 0.368 0.568
#&gt; SRR1946683     2  0.4897     0.6011 0.016 0.812 0.172
#&gt; SRR1946682     2  0.5327     0.4946 0.000 0.728 0.272
#&gt; SRR1946680     3  0.6410     0.4988 0.004 0.420 0.576
#&gt; SRR1946681     2  0.6434    -0.1077 0.008 0.612 0.380
#&gt; SRR1946687     3  0.6669     0.5177 0.008 0.468 0.524
#&gt; SRR1946679     2  0.5992     0.4124 0.016 0.716 0.268
#&gt; SRR1946678     1  0.0424     0.9350 0.992 0.008 0.000
#&gt; SRR1946676     2  0.0661     0.6958 0.008 0.988 0.004
#&gt; SRR1946677     2  0.1491     0.6937 0.016 0.968 0.016
#&gt; SRR1946672     3  0.6416     0.5675 0.008 0.376 0.616
#&gt; SRR1946673     3  0.6308    -0.0848 0.000 0.492 0.508
#&gt; SRR1946671     2  0.3896     0.6406 0.008 0.864 0.128
#&gt; SRR1946669     2  0.8623     0.3450 0.224 0.600 0.176
#&gt; SRR1946668     3  0.7164     0.3115 0.064 0.256 0.680
#&gt; SRR1946666     3  0.6027     0.5722 0.016 0.272 0.712
#&gt; SRR1946667     3  0.6386     0.5087 0.004 0.412 0.584
#&gt; SRR1946670     3  0.5905     0.3020 0.000 0.352 0.648
#&gt; SRR1946663     2  0.2200     0.6850 0.004 0.940 0.056
#&gt; SRR1946664     2  0.2261     0.6745 0.000 0.932 0.068
#&gt; SRR1946662     2  0.7903     0.3240 0.068 0.576 0.356
#&gt; SRR1946661     2  0.3715     0.6386 0.004 0.868 0.128
#&gt; SRR1946660     2  0.2165     0.6757 0.000 0.936 0.064
#&gt; SRR1946659     3  0.6138     0.5403 0.060 0.172 0.768
#&gt; SRR1946658     2  0.5948    -0.0623 0.000 0.640 0.360
#&gt; SRR1946657     2  0.2537     0.6427 0.000 0.920 0.080
#&gt; SRR1946655     3  0.6460     0.5419 0.004 0.440 0.556
#&gt; SRR1946654     3  0.6509     0.5176 0.004 0.472 0.524
#&gt; SRR1946653     3  0.5623     0.5741 0.004 0.280 0.716
#&gt; SRR1946652     2  0.6309     0.0420 0.000 0.500 0.500
#&gt; SRR1946651     2  0.5058     0.5289 0.000 0.756 0.244
#&gt; SRR1946650     2  0.1129     0.6937 0.004 0.976 0.020
#&gt; SRR1946649     2  0.1170     0.6952 0.008 0.976 0.016
#&gt; SRR1946648     2  0.6664    -0.4649 0.008 0.528 0.464
#&gt; SRR1946647     3  0.5928     0.3320 0.008 0.296 0.696
#&gt; SRR1946646     2  0.5122     0.3958 0.012 0.788 0.200
#&gt; SRR1946645     2  0.1636     0.6923 0.016 0.964 0.020
#&gt; SRR1946644     2  0.1182     0.6946 0.012 0.976 0.012
#&gt; SRR1946643     3  0.6577     0.5216 0.008 0.420 0.572
#&gt; SRR1946642     1  0.0661     0.9349 0.988 0.008 0.004
#&gt; SRR1946641     1  0.0661     0.9423 0.988 0.004 0.008
#&gt; SRR1946656     3  0.6330     0.5417 0.004 0.396 0.600
#&gt; SRR1946640     1  0.0661     0.9423 0.988 0.004 0.008
#&gt; SRR1946639     1  0.0661     0.9423 0.988 0.004 0.008
#&gt; SRR1946638     1  0.0661     0.9423 0.988 0.004 0.008
#&gt; SRR1946637     1  0.5480     0.5858 0.732 0.004 0.264
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     2  0.4955     0.4237 0.000 0.556 0.444 0.000
#&gt; SRR1946691     2  0.6677     0.4734 0.000 0.552 0.100 0.348
#&gt; SRR1946690     2  0.4977    -0.2669 0.000 0.540 0.000 0.460
#&gt; SRR1946689     4  0.5742     0.7314 0.000 0.036 0.368 0.596
#&gt; SRR1946686     3  0.7034     0.2776 0.364 0.112 0.520 0.004
#&gt; SRR1946685     2  0.3697     0.4918 0.000 0.852 0.100 0.048
#&gt; SRR1946688     2  0.4072     0.2676 0.000 0.748 0.000 0.252
#&gt; SRR1946684     3  0.7899     0.5713 0.040 0.120 0.504 0.336
#&gt; SRR1946683     2  0.5827    -0.2665 0.032 0.532 0.436 0.000
#&gt; SRR1946682     2  0.5324     0.4993 0.004 0.644 0.016 0.336
#&gt; SRR1946680     4  0.5742     0.7314 0.000 0.036 0.368 0.596
#&gt; SRR1946681     2  0.7583    -0.3468 0.004 0.432 0.168 0.396
#&gt; SRR1946687     2  0.4972     0.4153 0.000 0.544 0.456 0.000
#&gt; SRR1946679     2  0.2651     0.5397 0.004 0.896 0.096 0.004
#&gt; SRR1946678     1  0.0804     0.9759 0.980 0.008 0.012 0.000
#&gt; SRR1946676     2  0.0336     0.5470 0.000 0.992 0.000 0.008
#&gt; SRR1946677     2  0.3697     0.4918 0.000 0.852 0.100 0.048
#&gt; SRR1946672     2  0.5244     0.4232 0.008 0.556 0.436 0.000
#&gt; SRR1946673     2  0.6747     0.4729 0.004 0.556 0.092 0.348
#&gt; SRR1946671     2  0.0336     0.5465 0.000 0.992 0.008 0.000
#&gt; SRR1946669     3  0.8701     0.4858 0.180 0.068 0.464 0.288
#&gt; SRR1946668     3  0.7910     0.5703 0.040 0.120 0.500 0.340
#&gt; SRR1946666     3  0.3508     0.2945 0.012 0.136 0.848 0.004
#&gt; SRR1946667     4  0.5742     0.7314 0.000 0.036 0.368 0.596
#&gt; SRR1946670     2  0.6640     0.4718 0.000 0.552 0.096 0.352
#&gt; SRR1946663     2  0.4697     0.5195 0.000 0.696 0.008 0.296
#&gt; SRR1946664     4  0.4008     0.1430 0.000 0.244 0.000 0.756
#&gt; SRR1946662     3  0.8150     0.5698 0.052 0.128 0.496 0.324
#&gt; SRR1946661     2  0.4509     0.5219 0.000 0.708 0.004 0.288
#&gt; SRR1946660     2  0.5866     0.0369 0.000 0.624 0.052 0.324
#&gt; SRR1946659     3  0.2589     0.2995 0.000 0.116 0.884 0.000
#&gt; SRR1946658     2  0.6778     0.4752 0.000 0.552 0.112 0.336
#&gt; SRR1946657     2  0.5594     0.5205 0.004 0.672 0.040 0.284
#&gt; SRR1946655     2  0.4955     0.4237 0.000 0.556 0.444 0.000
#&gt; SRR1946654     2  0.5097     0.4293 0.004 0.568 0.428 0.000
#&gt; SRR1946653     2  0.5550     0.4262 0.000 0.552 0.428 0.020
#&gt; SRR1946652     2  0.6640     0.4718 0.000 0.552 0.096 0.352
#&gt; SRR1946651     2  0.4875     0.5169 0.004 0.692 0.008 0.296
#&gt; SRR1946650     2  0.4722     0.5196 0.000 0.692 0.008 0.300
#&gt; SRR1946649     2  0.1545     0.5495 0.000 0.952 0.008 0.040
#&gt; SRR1946648     2  0.4989     0.3996 0.000 0.528 0.472 0.000
#&gt; SRR1946647     2  0.7253     0.1134 0.000 0.520 0.308 0.172
#&gt; SRR1946646     2  0.5673     0.4247 0.000 0.596 0.372 0.032
#&gt; SRR1946645     2  0.3758     0.4922 0.000 0.848 0.104 0.048
#&gt; SRR1946644     2  0.1489     0.5318 0.000 0.952 0.004 0.044
#&gt; SRR1946643     4  0.7216     0.5691 0.000 0.140 0.412 0.448
#&gt; SRR1946642     1  0.0937     0.9739 0.976 0.012 0.012 0.000
#&gt; SRR1946641     1  0.0188     0.9806 0.996 0.000 0.004 0.000
#&gt; SRR1946656     3  0.7686    -0.4637 0.000 0.228 0.436 0.336
#&gt; SRR1946640     1  0.0188     0.9806 0.996 0.000 0.004 0.000
#&gt; SRR1946639     1  0.0000     0.9805 1.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     0.9805 1.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.1398     0.9518 0.956 0.000 0.040 0.004
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.4410     0.3664 0.000 0.004 0.556 0.000 0.440
#&gt; SRR1946691     5  0.0579     0.4777 0.000 0.008 0.008 0.000 0.984
#&gt; SRR1946690     2  0.6119     0.5004 0.000 0.672 0.080 0.140 0.108
#&gt; SRR1946689     3  0.7075     0.3290 0.000 0.080 0.500 0.324 0.096
#&gt; SRR1946686     1  0.5576     0.4445 0.536 0.000 0.388 0.000 0.076
#&gt; SRR1946685     4  0.5811     0.5471 0.000 0.140 0.000 0.596 0.264
#&gt; SRR1946688     2  0.5479     0.5234 0.000 0.724 0.080 0.068 0.128
#&gt; SRR1946684     5  0.6961     0.2724 0.128 0.052 0.304 0.000 0.516
#&gt; SRR1946683     2  0.9776     0.0115 0.224 0.252 0.248 0.124 0.152
#&gt; SRR1946682     5  0.4886     0.0583 0.000 0.448 0.000 0.024 0.528
#&gt; SRR1946680     3  0.7193     0.2378 0.000 0.080 0.412 0.412 0.096
#&gt; SRR1946681     3  0.8195     0.2531 0.000 0.168 0.384 0.160 0.288
#&gt; SRR1946687     3  0.6751     0.0692 0.000 0.004 0.424 0.220 0.352
#&gt; SRR1946679     5  0.8430    -0.2248 0.104 0.328 0.068 0.084 0.416
#&gt; SRR1946678     1  0.2086     0.8631 0.924 0.008 0.048 0.020 0.000
#&gt; SRR1946676     2  0.5210     0.5574 0.000 0.652 0.000 0.084 0.264
#&gt; SRR1946677     4  0.5770     0.5487 0.000 0.140 0.000 0.604 0.256
#&gt; SRR1946672     3  0.4383     0.3714 0.000 0.004 0.572 0.000 0.424
#&gt; SRR1946673     5  0.3496     0.4303 0.000 0.200 0.012 0.000 0.788
#&gt; SRR1946671     2  0.5340     0.6036 0.000 0.692 0.056 0.032 0.220
#&gt; SRR1946669     3  0.8157    -0.2598 0.300 0.276 0.348 0.012 0.064
#&gt; SRR1946668     5  0.6548     0.2832 0.124 0.032 0.288 0.000 0.556
#&gt; SRR1946666     3  0.5993     0.2232 0.248 0.000 0.580 0.000 0.172
#&gt; SRR1946667     3  0.7075     0.3290 0.000 0.080 0.500 0.324 0.096
#&gt; SRR1946670     5  0.0693     0.4803 0.000 0.000 0.008 0.012 0.980
#&gt; SRR1946663     2  0.3885     0.6066 0.000 0.724 0.000 0.008 0.268
#&gt; SRR1946664     2  0.6254     0.5031 0.000 0.660 0.080 0.136 0.124
#&gt; SRR1946662     3  0.8401    -0.2226 0.204 0.264 0.352 0.000 0.180
#&gt; SRR1946661     2  0.3582     0.5890 0.000 0.768 0.000 0.008 0.224
#&gt; SRR1946660     2  0.6236     0.4571 0.000 0.660 0.076 0.144 0.120
#&gt; SRR1946659     3  0.4026     0.3391 0.020 0.000 0.736 0.000 0.244
#&gt; SRR1946658     5  0.3699     0.3993 0.000 0.028 0.104 0.032 0.836
#&gt; SRR1946657     2  0.5161     0.3416 0.000 0.488 0.024 0.008 0.480
#&gt; SRR1946655     3  0.5495     0.3871 0.000 0.008 0.536 0.048 0.408
#&gt; SRR1946654     3  0.5065     0.3633 0.000 0.000 0.544 0.036 0.420
#&gt; SRR1946653     5  0.4658    -0.4032 0.000 0.000 0.484 0.012 0.504
#&gt; SRR1946652     5  0.4125     0.4723 0.000 0.224 0.004 0.024 0.748
#&gt; SRR1946651     2  0.4183     0.4171 0.000 0.668 0.000 0.008 0.324
#&gt; SRR1946650     2  0.3910     0.6068 0.000 0.720 0.000 0.008 0.272
#&gt; SRR1946649     2  0.4815     0.5932 0.000 0.692 0.000 0.064 0.244
#&gt; SRR1946648     4  0.7167     0.3623 0.000 0.024 0.220 0.420 0.336
#&gt; SRR1946647     5  0.4236     0.4378 0.012 0.020 0.164 0.016 0.788
#&gt; SRR1946646     4  0.7519     0.5501 0.000 0.108 0.112 0.452 0.328
#&gt; SRR1946645     4  0.5535     0.5534 0.000 0.116 0.000 0.628 0.256
#&gt; SRR1946644     2  0.7762     0.0567 0.000 0.392 0.064 0.296 0.248
#&gt; SRR1946643     4  0.7250    -0.1269 0.000 0.048 0.272 0.488 0.192
#&gt; SRR1946642     1  0.3056     0.8406 0.860 0.008 0.112 0.020 0.000
#&gt; SRR1946641     1  0.0162     0.8749 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946656     3  0.7086     0.3926 0.000 0.040 0.500 0.180 0.280
#&gt; SRR1946640     1  0.0162     0.8749 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946639     1  0.0000     0.8732 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0162     0.8749 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1946637     1  0.4010     0.7354 0.784 0.000 0.160 0.000 0.056
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.2344     0.6082 0.028 0.000 0.896 0.000 0.008 0.068
#&gt; SRR1946691     5  0.4573     0.5972 0.000 0.040 0.068 0.004 0.752 0.136
#&gt; SRR1946690     2  0.6839    -0.1463 0.000 0.384 0.052 0.188 0.004 0.372
#&gt; SRR1946689     4  0.2260     0.7597 0.000 0.000 0.140 0.860 0.000 0.000
#&gt; SRR1946686     1  0.3506     0.7315 0.792 0.000 0.052 0.000 0.156 0.000
#&gt; SRR1946685     2  0.2312     0.5758 0.000 0.876 0.012 0.000 0.000 0.112
#&gt; SRR1946688     6  0.6539     0.0712 0.000 0.336 0.048 0.168 0.000 0.448
#&gt; SRR1946684     5  0.2375     0.6121 0.060 0.008 0.000 0.000 0.896 0.036
#&gt; SRR1946683     1  0.8314     0.0867 0.392 0.200 0.028 0.028 0.132 0.220
#&gt; SRR1946682     6  0.4386    -0.2118 0.000 0.004 0.016 0.000 0.464 0.516
#&gt; SRR1946680     4  0.1621     0.7378 0.004 0.004 0.048 0.936 0.000 0.008
#&gt; SRR1946681     3  0.6365     0.1202 0.000 0.336 0.468 0.156 0.000 0.040
#&gt; SRR1946687     3  0.5645     0.4879 0.012 0.196 0.660 0.040 0.004 0.088
#&gt; SRR1946679     6  0.8586     0.0374 0.140 0.228 0.208 0.020 0.052 0.352
#&gt; SRR1946678     1  0.0891     0.8669 0.968 0.008 0.000 0.024 0.000 0.000
#&gt; SRR1946676     6  0.4427     0.4291 0.000 0.236 0.020 0.016 0.016 0.712
#&gt; SRR1946677     2  0.2313     0.5760 0.000 0.884 0.012 0.004 0.000 0.100
#&gt; SRR1946672     3  0.3474     0.6068 0.036 0.004 0.844 0.036 0.004 0.076
#&gt; SRR1946673     5  0.4568     0.5513 0.000 0.032 0.036 0.000 0.700 0.232
#&gt; SRR1946671     6  0.5276     0.4567 0.004 0.168 0.032 0.028 0.060 0.708
#&gt; SRR1946669     5  0.6453     0.0300 0.384 0.044 0.000 0.028 0.468 0.076
#&gt; SRR1946668     5  0.1562     0.6211 0.024 0.000 0.004 0.000 0.940 0.032
#&gt; SRR1946666     3  0.5335     0.3986 0.276 0.004 0.600 0.000 0.116 0.004
#&gt; SRR1946667     4  0.2340     0.7551 0.000 0.000 0.148 0.852 0.000 0.000
#&gt; SRR1946670     5  0.4514     0.6077 0.000 0.032 0.080 0.004 0.756 0.128
#&gt; SRR1946663     6  0.1956     0.5417 0.000 0.008 0.004 0.000 0.080 0.908
#&gt; SRR1946664     6  0.6451     0.2612 0.000 0.176 0.048 0.192 0.016 0.568
#&gt; SRR1946662     5  0.5567     0.2775 0.316 0.008 0.000 0.024 0.580 0.072
#&gt; SRR1946661     6  0.2592     0.5307 0.000 0.004 0.016 0.000 0.116 0.864
#&gt; SRR1946660     6  0.6156    -0.0236 0.000 0.420 0.048 0.100 0.000 0.432
#&gt; SRR1946659     3  0.2723     0.5710 0.016 0.000 0.852 0.000 0.128 0.004
#&gt; SRR1946658     3  0.7239     0.0384 0.000 0.104 0.372 0.000 0.308 0.216
#&gt; SRR1946657     6  0.4485     0.5018 0.000 0.084 0.028 0.064 0.040 0.784
#&gt; SRR1946655     3  0.3029     0.5433 0.000 0.008 0.852 0.088 0.000 0.052
#&gt; SRR1946654     3  0.5183     0.5303 0.004 0.032 0.692 0.148 0.000 0.124
#&gt; SRR1946653     3  0.4233     0.5039 0.004 0.000 0.720 0.000 0.216 0.060
#&gt; SRR1946652     5  0.4513     0.3711 0.000 0.004 0.032 0.000 0.596 0.368
#&gt; SRR1946651     6  0.3518     0.3453 0.000 0.000 0.012 0.000 0.256 0.732
#&gt; SRR1946650     6  0.1624     0.5424 0.000 0.008 0.012 0.000 0.044 0.936
#&gt; SRR1946649     6  0.4267     0.5177 0.000 0.136 0.024 0.012 0.052 0.776
#&gt; SRR1946648     2  0.7197     0.2082 0.004 0.452 0.248 0.168 0.000 0.128
#&gt; SRR1946647     5  0.4381     0.6185 0.004 0.040 0.068 0.004 0.780 0.104
#&gt; SRR1946646     2  0.6465     0.4205 0.004 0.580 0.156 0.128 0.000 0.132
#&gt; SRR1946645     2  0.2375     0.5788 0.000 0.888 0.012 0.012 0.000 0.088
#&gt; SRR1946644     2  0.6360     0.1361 0.000 0.540 0.048 0.160 0.004 0.248
#&gt; SRR1946643     4  0.5974     0.3178 0.000 0.344 0.132 0.500 0.000 0.024
#&gt; SRR1946642     1  0.1518     0.8539 0.944 0.008 0.000 0.024 0.024 0.000
#&gt; SRR1946641     1  0.0260     0.8734 0.992 0.000 0.008 0.000 0.000 0.000
#&gt; SRR1946656     3  0.5203    -0.0449 0.000 0.056 0.560 0.364 0.000 0.020
#&gt; SRR1946640     1  0.0363     0.8723 0.988 0.000 0.012 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     0.8723 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0146     0.8734 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR1946637     1  0.1152     0.8560 0.952 0.000 0.044 0.000 0.004 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 17231 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.946       0.979         0.3360 0.665   0.665
#> 3 3 0.607           0.705       0.883         0.8451 0.637   0.487
#> 4 4 0.689           0.788       0.891         0.1968 0.765   0.461
#> 5 5 0.658           0.691       0.818         0.0825 0.866   0.541
#> 6 6 0.722           0.627       0.753         0.0493 0.896   0.547
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1946675     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946691     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946690     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946689     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946686     1  0.0376      0.944 0.996 0.004
#&gt; SRR1946685     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946688     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946684     2  0.9977      0.021 0.472 0.528
#&gt; SRR1946683     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946682     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946680     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946681     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946687     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946679     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946678     1  0.0000      0.946 1.000 0.000
#&gt; SRR1946676     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946677     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946672     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946673     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946671     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946669     1  0.0000      0.946 1.000 0.000
#&gt; SRR1946668     2  0.2236      0.949 0.036 0.964
#&gt; SRR1946666     2  0.3274      0.923 0.060 0.940
#&gt; SRR1946667     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946670     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946663     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946664     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946662     1  0.7453      0.737 0.788 0.212
#&gt; SRR1946661     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946660     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946659     1  0.8909      0.575 0.692 0.308
#&gt; SRR1946658     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946657     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946655     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946654     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946653     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946652     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946651     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946650     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946649     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946648     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946647     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946646     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946645     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946644     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946643     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946642     1  0.0000      0.946 1.000 0.000
#&gt; SRR1946641     1  0.0000      0.946 1.000 0.000
#&gt; SRR1946656     2  0.0000      0.985 0.000 1.000
#&gt; SRR1946640     1  0.0000      0.946 1.000 0.000
#&gt; SRR1946639     1  0.0000      0.946 1.000 0.000
#&gt; SRR1946638     1  0.0000      0.946 1.000 0.000
#&gt; SRR1946637     1  0.0000      0.946 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1946675     3  0.0000    0.83362 0.000 0.000 1.000
#&gt; SRR1946691     3  0.4121    0.73443 0.000 0.168 0.832
#&gt; SRR1946690     2  0.1860    0.80098 0.000 0.948 0.052
#&gt; SRR1946689     2  0.6309   -0.00626 0.000 0.504 0.496
#&gt; SRR1946686     3  0.2878    0.76652 0.096 0.000 0.904
#&gt; SRR1946685     2  0.0237    0.82858 0.000 0.996 0.004
#&gt; SRR1946688     2  0.0237    0.82858 0.000 0.996 0.004
#&gt; SRR1946684     2  0.9606    0.12123 0.352 0.440 0.208
#&gt; SRR1946683     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946682     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946680     2  0.5859    0.38762 0.000 0.656 0.344
#&gt; SRR1946681     3  0.5650    0.54253 0.000 0.312 0.688
#&gt; SRR1946687     3  0.0237    0.83314 0.000 0.004 0.996
#&gt; SRR1946679     2  0.6111    0.25387 0.000 0.604 0.396
#&gt; SRR1946678     1  0.0000    0.94773 1.000 0.000 0.000
#&gt; SRR1946676     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946677     2  0.0424    0.82809 0.000 0.992 0.008
#&gt; SRR1946672     3  0.0000    0.83362 0.000 0.000 1.000
#&gt; SRR1946673     2  0.6225    0.14011 0.000 0.568 0.432
#&gt; SRR1946671     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946669     1  0.5529    0.52601 0.704 0.296 0.000
#&gt; SRR1946668     2  0.9464   -0.08999 0.180 0.412 0.408
#&gt; SRR1946666     3  0.0237    0.83199 0.004 0.000 0.996
#&gt; SRR1946667     3  0.5254    0.56142 0.000 0.264 0.736
#&gt; SRR1946670     3  0.6140    0.30725 0.000 0.404 0.596
#&gt; SRR1946663     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946664     2  0.0892    0.82172 0.000 0.980 0.020
#&gt; SRR1946662     2  0.5465    0.53171 0.288 0.712 0.000
#&gt; SRR1946661     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946660     2  0.0237    0.82858 0.000 0.996 0.004
#&gt; SRR1946659     3  0.0237    0.83199 0.004 0.000 0.996
#&gt; SRR1946658     3  0.6062    0.35512 0.000 0.384 0.616
#&gt; SRR1946657     2  0.0237    0.82816 0.000 0.996 0.004
#&gt; SRR1946655     3  0.0000    0.83362 0.000 0.000 1.000
#&gt; SRR1946654     3  0.1031    0.82811 0.000 0.024 0.976
#&gt; SRR1946653     3  0.0000    0.83362 0.000 0.000 1.000
#&gt; SRR1946652     2  0.4750    0.61629 0.000 0.784 0.216
#&gt; SRR1946651     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946650     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946649     2  0.0000    0.82917 0.000 1.000 0.000
#&gt; SRR1946648     3  0.5650    0.54107 0.000 0.312 0.688
#&gt; SRR1946647     3  0.0592    0.83153 0.000 0.012 0.988
#&gt; SRR1946646     2  0.5098    0.56341 0.000 0.752 0.248
#&gt; SRR1946645     2  0.0592    0.82651 0.000 0.988 0.012
#&gt; SRR1946644     2  0.2066    0.79489 0.000 0.940 0.060
#&gt; SRR1946643     3  0.4605    0.68477 0.000 0.204 0.796
#&gt; SRR1946642     1  0.0000    0.94773 1.000 0.000 0.000
#&gt; SRR1946641     1  0.0000    0.94773 1.000 0.000 0.000
#&gt; SRR1946656     3  0.0000    0.83362 0.000 0.000 1.000
#&gt; SRR1946640     1  0.0000    0.94773 1.000 0.000 0.000
#&gt; SRR1946639     1  0.0000    0.94773 1.000 0.000 0.000
#&gt; SRR1946638     1  0.0000    0.94773 1.000 0.000 0.000
#&gt; SRR1946637     1  0.0000    0.94773 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1946675     3  0.2530      0.765 0.000 0.000 0.888 0.112
#&gt; SRR1946691     4  0.1022      0.871 0.000 0.000 0.032 0.968
#&gt; SRR1946690     2  0.0804      0.885 0.000 0.980 0.012 0.008
#&gt; SRR1946689     3  0.4872      0.435 0.000 0.356 0.640 0.004
#&gt; SRR1946686     1  0.5619      0.666 0.724 0.000 0.124 0.152
#&gt; SRR1946685     2  0.1389      0.873 0.000 0.952 0.048 0.000
#&gt; SRR1946688     2  0.0336      0.884 0.000 0.992 0.000 0.008
#&gt; SRR1946684     4  0.0524      0.880 0.004 0.000 0.008 0.988
#&gt; SRR1946683     2  0.1762      0.869 0.004 0.944 0.004 0.048
#&gt; SRR1946682     4  0.2469      0.848 0.000 0.108 0.000 0.892
#&gt; SRR1946680     2  0.3801      0.679 0.000 0.780 0.220 0.000
#&gt; SRR1946681     3  0.5055      0.405 0.000 0.368 0.624 0.008
#&gt; SRR1946687     3  0.0336      0.779 0.000 0.008 0.992 0.000
#&gt; SRR1946679     2  0.7740      0.197 0.000 0.432 0.248 0.320
#&gt; SRR1946678     1  0.0000      0.962 1.000 0.000 0.000 0.000
#&gt; SRR1946676     2  0.0188      0.884 0.000 0.996 0.000 0.004
#&gt; SRR1946677     2  0.1637      0.868 0.000 0.940 0.060 0.000
#&gt; SRR1946672     3  0.1211      0.784 0.000 0.000 0.960 0.040
#&gt; SRR1946673     4  0.0672      0.882 0.000 0.008 0.008 0.984
#&gt; SRR1946671     2  0.1867      0.858 0.000 0.928 0.000 0.072
#&gt; SRR1946669     4  0.3808      0.776 0.176 0.012 0.000 0.812
#&gt; SRR1946668     4  0.0188      0.881 0.000 0.000 0.004 0.996
#&gt; SRR1946666     3  0.0817      0.785 0.000 0.000 0.976 0.024
#&gt; SRR1946667     3  0.3591      0.708 0.000 0.168 0.824 0.008
#&gt; SRR1946670     4  0.0592      0.878 0.000 0.000 0.016 0.984
#&gt; SRR1946663     4  0.4356      0.639 0.000 0.292 0.000 0.708
#&gt; SRR1946664     2  0.0937      0.885 0.000 0.976 0.012 0.012
#&gt; SRR1946662     4  0.3421      0.839 0.088 0.044 0.000 0.868
#&gt; SRR1946661     4  0.3688      0.771 0.000 0.208 0.000 0.792
#&gt; SRR1946660     2  0.0469      0.884 0.000 0.988 0.012 0.000
#&gt; SRR1946659     3  0.3307      0.753 0.028 0.000 0.868 0.104
#&gt; SRR1946658     4  0.3266      0.728 0.000 0.000 0.168 0.832
#&gt; SRR1946657     2  0.3837      0.678 0.000 0.776 0.000 0.224
#&gt; SRR1946655     3  0.2647      0.759 0.000 0.000 0.880 0.120
#&gt; SRR1946654     3  0.1042      0.785 0.000 0.008 0.972 0.020
#&gt; SRR1946653     3  0.4040      0.648 0.000 0.000 0.752 0.248
#&gt; SRR1946652     4  0.0657      0.882 0.000 0.012 0.004 0.984
#&gt; SRR1946651     4  0.3528      0.790 0.000 0.192 0.000 0.808
#&gt; SRR1946650     2  0.2973      0.795 0.000 0.856 0.000 0.144
#&gt; SRR1946649     2  0.0592      0.882 0.000 0.984 0.000 0.016
#&gt; SRR1946648     3  0.4855      0.322 0.000 0.400 0.600 0.000
#&gt; SRR1946647     4  0.0817      0.876 0.000 0.000 0.024 0.976
#&gt; SRR1946646     2  0.2530      0.824 0.000 0.888 0.112 0.000
#&gt; SRR1946645     2  0.1867      0.860 0.000 0.928 0.072 0.000
#&gt; SRR1946644     2  0.0469      0.884 0.000 0.988 0.012 0.000
#&gt; SRR1946643     3  0.4746      0.405 0.000 0.368 0.632 0.000
#&gt; SRR1946642     1  0.0000      0.962 1.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000      0.962 1.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0895      0.786 0.000 0.004 0.976 0.020
#&gt; SRR1946640     1  0.0000      0.962 1.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.962 1.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.962 1.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.962 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1946675     3  0.2414      0.783 0.000 0.012 0.900 0.008 0.080
#&gt; SRR1946691     5  0.3971      0.754 0.000 0.008 0.136 0.052 0.804
#&gt; SRR1946690     4  0.1205      0.770 0.000 0.040 0.000 0.956 0.004
#&gt; SRR1946689     4  0.2228      0.770 0.000 0.008 0.068 0.912 0.012
#&gt; SRR1946686     1  0.3929      0.745 0.788 0.000 0.036 0.004 0.172
#&gt; SRR1946685     2  0.2707      0.627 0.000 0.860 0.008 0.132 0.000
#&gt; SRR1946688     4  0.0992      0.778 0.000 0.024 0.000 0.968 0.008
#&gt; SRR1946684     5  0.0162      0.840 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1946683     2  0.4733      0.624 0.008 0.752 0.000 0.116 0.124
#&gt; SRR1946682     5  0.3246      0.702 0.000 0.008 0.000 0.184 0.808
#&gt; SRR1946680     4  0.1106      0.782 0.000 0.012 0.024 0.964 0.000
#&gt; SRR1946681     3  0.4717      0.252 0.000 0.396 0.584 0.020 0.000
#&gt; SRR1946687     3  0.5271      0.602 0.000 0.152 0.680 0.168 0.000
#&gt; SRR1946679     2  0.3387      0.616 0.000 0.836 0.024 0.008 0.132
#&gt; SRR1946678     1  0.0000      0.969 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     2  0.3715      0.626 0.000 0.736 0.000 0.260 0.004
#&gt; SRR1946677     2  0.3676      0.571 0.000 0.760 0.004 0.232 0.004
#&gt; SRR1946672     3  0.2574      0.774 0.000 0.112 0.876 0.000 0.012
#&gt; SRR1946673     5  0.3632      0.766 0.000 0.176 0.020 0.004 0.800
#&gt; SRR1946671     2  0.4341      0.556 0.000 0.628 0.000 0.364 0.008
#&gt; SRR1946669     5  0.4355      0.747 0.164 0.076 0.000 0.000 0.760
#&gt; SRR1946668     5  0.0162      0.840 0.000 0.000 0.000 0.004 0.996
#&gt; SRR1946666     3  0.3672      0.756 0.072 0.056 0.848 0.020 0.004
#&gt; SRR1946667     4  0.4905      0.405 0.000 0.008 0.344 0.624 0.024
#&gt; SRR1946670     5  0.1168      0.840 0.000 0.008 0.032 0.000 0.960
#&gt; SRR1946663     4  0.4283      0.456 0.000 0.008 0.000 0.644 0.348
#&gt; SRR1946664     4  0.2236      0.747 0.000 0.068 0.000 0.908 0.024
#&gt; SRR1946662     5  0.3506      0.811 0.064 0.104 0.000 0.000 0.832
#&gt; SRR1946661     5  0.2592      0.812 0.000 0.056 0.000 0.052 0.892
#&gt; SRR1946660     4  0.2848      0.672 0.000 0.156 0.000 0.840 0.004
#&gt; SRR1946659     3  0.1788      0.787 0.000 0.008 0.932 0.004 0.056
#&gt; SRR1946658     5  0.3224      0.764 0.000 0.016 0.160 0.000 0.824
#&gt; SRR1946657     2  0.4198      0.640 0.000 0.792 0.016 0.144 0.048
#&gt; SRR1946655     3  0.1845      0.787 0.000 0.016 0.928 0.000 0.056
#&gt; SRR1946654     2  0.4709      0.229 0.000 0.584 0.400 0.008 0.008
#&gt; SRR1946653     3  0.3392      0.750 0.000 0.064 0.848 0.004 0.084
#&gt; SRR1946652     5  0.4920      0.493 0.000 0.348 0.024 0.008 0.620
#&gt; SRR1946651     2  0.5470      0.568 0.000 0.680 0.008 0.152 0.160
#&gt; SRR1946650     2  0.4371      0.567 0.000 0.644 0.000 0.344 0.012
#&gt; SRR1946649     2  0.4341      0.525 0.000 0.592 0.000 0.404 0.004
#&gt; SRR1946648     2  0.5793      0.215 0.000 0.584 0.292 0.124 0.000
#&gt; SRR1946647     5  0.0794      0.840 0.000 0.000 0.028 0.000 0.972
#&gt; SRR1946646     2  0.4192      0.576 0.000 0.736 0.032 0.232 0.000
#&gt; SRR1946645     2  0.4505      0.325 0.000 0.604 0.012 0.384 0.000
#&gt; SRR1946644     2  0.4251      0.572 0.000 0.624 0.004 0.372 0.000
#&gt; SRR1946643     3  0.5927      0.400 0.000 0.340 0.540 0.120 0.000
#&gt; SRR1946642     1  0.0000      0.969 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000      0.969 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0451      0.787 0.000 0.008 0.988 0.000 0.004
#&gt; SRR1946640     1  0.0000      0.969 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000      0.969 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000      0.969 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000      0.969 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1946675     3  0.1332     0.7497 0.000 0.008 0.952 0.000 0.012 0.028
#&gt; SRR1946691     6  0.5952     0.4812 0.000 0.056 0.108 0.256 0.000 0.580
#&gt; SRR1946690     4  0.2003     0.7000 0.000 0.116 0.000 0.884 0.000 0.000
#&gt; SRR1946689     4  0.2453     0.7491 0.000 0.000 0.044 0.896 0.044 0.016
#&gt; SRR1946686     6  0.4899     0.2810 0.392 0.004 0.036 0.004 0.004 0.560
#&gt; SRR1946685     5  0.3608     0.7548 0.000 0.248 0.000 0.012 0.736 0.004
#&gt; SRR1946688     4  0.1605     0.7599 0.000 0.016 0.000 0.936 0.044 0.004
#&gt; SRR1946684     6  0.0914     0.7445 0.000 0.016 0.000 0.000 0.016 0.968
#&gt; SRR1946683     5  0.4764     0.7042 0.000 0.232 0.000 0.000 0.660 0.108
#&gt; SRR1946682     6  0.3189     0.6207 0.000 0.004 0.000 0.236 0.000 0.760
#&gt; SRR1946680     4  0.2279     0.7618 0.000 0.024 0.016 0.904 0.056 0.000
#&gt; SRR1946681     3  0.5775     0.0739 0.000 0.104 0.468 0.020 0.408 0.000
#&gt; SRR1946687     3  0.5742     0.2013 0.000 0.028 0.456 0.084 0.432 0.000
#&gt; SRR1946679     5  0.4952     0.6662 0.000 0.252 0.000 0.000 0.632 0.116
#&gt; SRR1946678     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946676     2  0.3718     0.5849 0.000 0.784 0.000 0.132 0.084 0.000
#&gt; SRR1946677     5  0.2668     0.7959 0.000 0.168 0.000 0.000 0.828 0.004
#&gt; SRR1946672     3  0.3217     0.6313 0.000 0.008 0.768 0.000 0.224 0.000
#&gt; SRR1946673     2  0.5034    -0.0532 0.000 0.532 0.056 0.000 0.008 0.404
#&gt; SRR1946671     2  0.4212     0.3310 0.000 0.560 0.000 0.424 0.016 0.000
#&gt; SRR1946669     6  0.3610     0.7041 0.052 0.088 0.000 0.000 0.036 0.824
#&gt; SRR1946668     6  0.0405     0.7467 0.000 0.008 0.000 0.004 0.000 0.988
#&gt; SRR1946666     3  0.5487     0.5764 0.204 0.016 0.660 0.016 0.100 0.004
#&gt; SRR1946667     4  0.3652     0.6350 0.000 0.000 0.212 0.760 0.008 0.020
#&gt; SRR1946670     6  0.2220     0.7416 0.000 0.052 0.020 0.020 0.000 0.908
#&gt; SRR1946663     6  0.4097     0.0959 0.000 0.008 0.000 0.492 0.000 0.500
#&gt; SRR1946664     4  0.2946     0.6125 0.000 0.184 0.000 0.808 0.004 0.004
#&gt; SRR1946662     6  0.4508     0.5400 0.040 0.280 0.000 0.000 0.012 0.668
#&gt; SRR1946661     6  0.2643     0.7131 0.000 0.128 0.000 0.008 0.008 0.856
#&gt; SRR1946660     4  0.4282     0.3082 0.000 0.020 0.000 0.560 0.420 0.000
#&gt; SRR1946659     3  0.1088     0.7511 0.016 0.024 0.960 0.000 0.000 0.000
#&gt; SRR1946658     6  0.4556     0.6003 0.000 0.056 0.220 0.008 0.008 0.708
#&gt; SRR1946657     2  0.2949     0.4988 0.000 0.848 0.028 0.000 0.116 0.008
#&gt; SRR1946655     3  0.0713     0.7520 0.000 0.028 0.972 0.000 0.000 0.000
#&gt; SRR1946654     2  0.4499     0.0241 0.000 0.540 0.428 0.000 0.032 0.000
#&gt; SRR1946653     3  0.2402     0.6841 0.004 0.140 0.856 0.000 0.000 0.000
#&gt; SRR1946652     2  0.3348     0.5224 0.000 0.836 0.036 0.000 0.028 0.100
#&gt; SRR1946651     2  0.1946     0.6020 0.000 0.912 0.000 0.072 0.004 0.012
#&gt; SRR1946650     2  0.4109     0.3508 0.000 0.576 0.000 0.412 0.012 0.000
#&gt; SRR1946649     2  0.4322     0.2767 0.000 0.528 0.000 0.452 0.020 0.000
#&gt; SRR1946648     5  0.1975     0.7522 0.000 0.020 0.028 0.012 0.928 0.012
#&gt; SRR1946647     6  0.0508     0.7465 0.000 0.000 0.000 0.012 0.004 0.984
#&gt; SRR1946646     5  0.3050     0.7876 0.000 0.136 0.004 0.028 0.832 0.000
#&gt; SRR1946645     5  0.1720     0.7594 0.000 0.032 0.000 0.040 0.928 0.000
#&gt; SRR1946644     2  0.4475     0.5342 0.000 0.692 0.000 0.220 0.088 0.000
#&gt; SRR1946643     5  0.3373     0.6024 0.000 0.012 0.140 0.032 0.816 0.000
#&gt; SRR1946642     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946641     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946656     3  0.0767     0.7548 0.000 0.012 0.976 0.004 0.008 0.000
#&gt; SRR1946640     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946639     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946638     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1946637     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


