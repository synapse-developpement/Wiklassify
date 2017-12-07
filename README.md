# Wiklassify - Detection of Textual Incoherences project

This repository concerns the pieces of work related to detection of textual incoherences based on text samples retrieved from French Wikipedia dumps.

## Repository content

* Jupyter notebooks (with Python 3)
* Datasets<br>
   <code>XX-meta-historyX.xml-pXXXXpXXXX.tsv</code> files obtained from <code>.xml</code> from French Wikipedia dumps<br>
   <code>XX_XX_sample.tsv</code> annotated datasets with labels <code>XX_XX_post_annot.csv</code>

### Data

Wikipedia dump xml files are downloaded from https://dumps.wikimedia.org/frwiki/20170801/ (obsolete link, similar content in https://dumps.wikimedia.org/frwiki/20171201/, all history versions are available at https://dumps.wikimedia.org/frwiki/). Each compressed part of the edit history can be obtained and extracted with the following lines of code:

```
wget https://dumps.wikimedia.org/frwiki/20171001/frwiki-20171001-pages-meta-history1.xml-p3p3581.7z
7z x frwiki-20171001-pages-meta-history1.xml-p3p3581.7z
```

### Notebooks

* nb1_xml_extractor.ipynb

> Extracts modifications between two consecutive edits from <code>.xml</code> files and turn all samples into a pandas dataframe saved as a <code>XX-meta-historyX.xml-pXXXXpXXXX.tsv</code> file stored in folder <code>/tsv_output</code>. Each output file contains around 1.5 million pairs of text versions. An input <code>.xml</code> file has an average compressed volume of 250 MB that rises to around 28 GB when decompressed. The average time for extracting version pairs is 5 hours (median is 3 hours).
    
* nb2_tsv_sampling.ipynb

> For each <code>.tsv</code> file, filter irrelevant edits and randomly draw samples from a few files in order to generate small datasets of 100 text version pairs that are stored in two ways: <code>XX_XX_pre_annot.csv</code> for human annotation tasks and <code>XX_XX_sample.tsv</code> for experiments on jupyter notebooks. They are saved in <code>annotations</code> folder.

* nb3_visualizer_annotator.ipynb

> Visualizes the content of each set of 100 text version pairs and assists the annotator in labelling each sample with **InterfaceAnnotation.exe**. For using that software, one needs to load <code>/path/classes.csv</code> as *Classification plan* and <code>/path/XX_XX_pre_annot.csv</code> as *Corpus CSV file*. Then it suffices to tick the boxes corresponding to relevant labels for each observation on the left panel. The right panel displays the sample_id for ensuring that the annotator is labelling the right observation. After each session, the labelling software returns a new file renamed <code>XX_XX_post_annot.csv</code> and stored in <code>annotations</code> folder. One observation can be tagged with one or more of 14 labels.

![alt text](https://github.com/synapse-developpement/Wiklassify/raw/master/data/annotation_kit/Capture.PNG)

* nb4_multilabelling_classification.ipynb

> Attempts to identify edits related to semantic modifications. The goal is to increase the number of semantics-related edits through a semi-supervised approach.

* nb5_detection_semantic_incoherences.ipynb

> Within hand-labeled semantics-related text version pairs, each text fragment is set apart as a single observation. The goal consists in building a model that can identify an incoherence from a single text sample.

## Built With

* [Gensim](https://radimrehurek.com/gensim/) - Python library for language modelling

## Contributing

Please read [CONTRIBUTING.md](https://github.com/synapse-developpement/Wiklassify/blob/master/CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Author

**Olivier Salaün**

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
