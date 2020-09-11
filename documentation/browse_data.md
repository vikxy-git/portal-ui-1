<a name="top"></a>

# The HMPDACC Portal

The [HMPDACC Portal](http://portal.hmpdacc.org/) provides a summary of available data, as well as faceted and advanced search tools to identify data of interest. 

![HMPDACC portal home page](images/nemo_data_portal/nemo-main-landing-page.png)

The portal landing page is broken up into 3 section:
 * The welcome box provides your entry to querying data, described in more detail immediately below.
 * A bar graph breaks down number of samples per body site across all HMP projects.
 * The data portal summary bar at the bottom provides a high level summary of all data currently available through the HMPDACC portal.
 
### The Welcome Box

Begin exploring data by study or through the faceted or advanced search options. The `studies` button takes users to a summary page listing available studies, with links to all samples or all files associated with the study.

The `data` button will take you to the faceted data search page, the heart of the portal's functionality, described immediately below.

Below these are a set of pre-defined, commonly accessed queries. As an example, one can easily retreive all files associated with stool samples.


### Faceted Search Page

The HMPDACC Data Portal provides a simple faceted search query interface to help identify data of interest. The faceted search page, accessible through the `Data` button in the landing page welcome box, is divided into 3 sections: the filter panel, the advanced search box and the summary results panel. 

The filter panel on the left allows users to select one or more of the available facets to filter down the samples of interest (See #1 in figure). Selecting any facet automatically populates the advanced search box with the current query (See #2 in figure). The summary results panel provides dynamic pie charts summarizing data corresponding to the currently selected filters (See #3 in figure).

![NeMO data landing page](images/nemo_data_portal/nemo-data-landing-page.png)

The filter panel contains two tabs of pre-configured facets associated with 
* samples (project, body site, studies, gender), or 
* files (format, data type, annotation pipeline, matrix type) 

The number next to each facet corresponds to the number of samples associated with this attribute across *all* projects in the portal. This number does not change dynamically as facets are selected or deselected. What does change is the summary results panel. As facets are selected, the file count, sample count and file size total will update to reflect the current filter(s). The pie charts will also update to reflect the current filter(s). Hovering over any of the pie charts will show a table of counts of files and total file size for each component of the pie chart. This table is also accessible by clicking on the table icon in the upper right corner of the pie chart to toggle between chart or table views.  

In addition to filtering via the filter panel, users can click directly on a pie piece or table field to dig further into a specific component of the dataset. Once data has been refined to the dataset of interest, click on the **Files** tab of the summary results panel. From here, files can be added to the shopping cart, as described below. 

Additional facets are available by ***Add a Filter*** in the upper right of the filter panel. The resulting pop-up lists all additional searchable facets available, which can be browsed or searched for using the search bar at the top. Clicking on any facet will add it to the top of the filter panel for incorporation into the current filter.

#### Example query
Professor Julia is interested in running a beta-diversity analysis comparing her own, personal stool samples from patients with a particular IBD phenotype, to healthy human stool samples from the HMP. Given that she will be running her own analysis tools, she is interested only in raw data from HMP. Starting at [portal.hmpdacc.org/](https://portal.hmpdacc.org/), she takes the following steps:
1) Click the `Data` button at the top of the page to access the faceted search page
2) In the Samples filter panel, select "feces" in the Body Site category AND "HHS" in the Studies category, in order to select only data from Healthy Human Subjects.
3) In the Files filter panel, select "wgs_raw_seq_set" in the Type category. This further narrows the search to only raw FASTQ files. This filter could also have been applied from the pie chart summary panel.

![NeMO select some data](images/nemo_data_portal/nemo-data-select-study.png)

4) Click the Files tab and add all files to the data cart by clicking on the arrow next to the cart icon at the top of the Files box, and selecting 'Add all files to the cart'. Note that there is a 10,000 file data cart limit.
Instructions for downloading files from the data cart are below. 

[top](#top)

### Advanced Search 

The Advanced Search feature simulates querying a database directly. To begin an advanced search, click the "Advanced" button in the upper right corner of the advanced search box. 

![NeMO Advanced Search button](images/nemo_data_portal/advanced-search.png)

A query requires the following basic format:

```bash
(property) (comparison operator) (value)
```

The property is what you're searching on, ie the facet. The comparison operator is how you want to relate your value to your property, ie equals, in. The value is what you're filtering the property on.

For example:
**sample.body_site = feces OR sample.body_site in [feces, colon]** 
![NeMO Advanced Query](images/nemo_data_portal/advanced-query.png)

Clicking "Submit Query" will update the summary results panel in the same way as the faceted search. 

Auto-complete helps in entering an advanced query. Auto-complete will pull all valid options directly from the database to ensure that a user's search contains a valid property, comparison operator, and value. If auto-complete suggests no results in your query, you have likely entered nonexistent combinations of property+comparison operator+value. The auto-complete feature is also helpful in that it allows users to browse all current values in the database for that particular property.

[top](#top)

### Adding Files To Shopping Cart <a name="add-to-shopping-cart"></a>
Once data has been refined to the dataset of interest, click on the **Files** tab of the summary results panel. This will bring up the list of files matching the search criterion. The files list table provides some basic information about the file including access type, URL, data category, file format, and size.

![Add files to shopping cart](images/nemo_data_portal/nemo-add-to-shopping-cart.png)

Clicking on an individual file takes users to a summary page for the selected file, with the option to download via the `Download` button in the upper right. 

![Indivdual file information](images/nemo_data_portal/nemo-file-list-item-details.png)

To download multiple files, users can either click on the shopping cart icon to the left of all files of interest or select the shopping cart dropdown arrow at the top left of the Files table and select **Add all files to the Cart**. Note that there is a 10,000 file data cart limit. Files in excess of this number would need to be added to an empty cart and downloaded as a second download process.

The cart icon on the top right of the page will display the number of items currently in the cart. At this point, users can continue to browse for additional files, combine results of multiple queries, or proceed to the cart page to download the selected files. 

[top](#top)

### Downloading files from the Data Cart  <a name="download-from-cart"></a>
Clicking on the cart icon on the top right of the page takes users to the Data Cart. At the top is a summary of the files currently in the cart. 

Downloading and analyzing large files can be very resource intensive and so it is recommended to use the HMP portal client for this purpose. 
The HMP portal client is a Python-based client run on the command line. It can be installed using easy_install, pip, VirtualEnv or docker. Installation instructions are [available here](https://github.com/IGS/portal_client/blob/master/INSTALL.md).

In order to use the portal client, users must first download 1) a file manifest and 2) a sample metadata file using the 'Download' dropdown in the upper right of the Cart Items table. These two files can be joined on the sample_id column. Basic invocation of the portal client requires simple specifying the path to the file manifest using the `-m` or `--manifest` option

```bash
portal_client --manifest /path/to/my/manifest.tsv
```
Detailed portal client documentation is [available here](https://github.com/IGS/portal_client/blob/master/README.md). 

