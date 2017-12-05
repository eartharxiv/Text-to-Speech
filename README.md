Requirements and Background
-------

This code has additional Python libraries on which it depends.

For text-to-speach, we're using <a href="https://pypi.python.org/pypi/gTTS">Google Text-To-Speech (gTTS)</a> version 1.2.2 installed via pip
```python
pip install gTTS
``` 

This example was initially created to demonstrate converting EarthArXiv preprints to speech. As such, the code currently focuses exclusively on PDF to Text to Speech as PDF is what is returned from the EarthArXiv API. The PDF to text I use pdfminer, which has an excellent tutorial <a href="
http://stanford.edu/~mgorkove/cgi-bin/rpython_tutorials/Using%20Python%20to%20Convert%20PDFs%20to%20Text%20Files.php">here</a>. Note that pdfminer is only available for python2.

I use the <a href="https://github.com/eartharxiv/API">EarthArXiv Python API code</a> to retrieve a preprint in PDF format. I then use pdf2mp3.py in this repository to convert the PDF to mp3.

Known Issues
-----------

This project is still very much under development. A number of know issues exist that we hope to resolve over in future releases.

1.) Currently, we are only focused on PDF files as they are what is returned from the EarthArXiv API. No support currently exists for converting other formats to speech.

2.) My initial interest was to listen to preprints on my commute. As such, the current version outputs an mp3 file that I transfer to my iPod. Future versions will look at playing the audio directly within a Python application.

3.) Not really an issue, more something I'd like to look into. Nic Weber has a nice speech-to-text <a href="https://github.com/CouncilDataProject/transcription_runner/blob/master/python/simple_transcription.py">code</a>. I'd love to explore capturing preprint comments via this code and converting them to text, which could then be sent back to EarthArXiv.

4.) The conversion to mp3 is a bit clunky at the moment. Text-to-Speech simply reads the document linearly from top to bottom. This raises the following issues (and probably a few others I haven't found yet)
	a.) if a figure or table is embedded in the text, which it almost always is for science documents, the text-to-speech will jump from the main text to the figure caption and back. This is confusing to a listener.
	b.) science papers are often formatted two-columns, which leads to words being hyphonated as they are wrapped on the page. Text-to-speech has trouble with hyponated words that normally aren't hyphonated

I think 4.) can be addressed with some pre-processing of the text prior to converting it to mp3, i.e. go from PDF to text, remove figures/captions/table, format hypons, then convert to mp3. Just haven't had time to explore this yet.
