# pdf4py
A PDF parser written in Python 3 with no external dependencies.

The package `pdf4py` allows the user to analyze a PDF file at a very low level and in a very
flexible way by giving access to its atomic components, the PDF objects. All through a very
simple API that can be used to build higher level functionalities (e.g. text and/or image
extraction). In particular, it defines the class `Parser` that reads the *Cross Reference Table*
of a PDF document and uses its entries to give the user the ability to locate PDF objects within
the file and parse them into suitable Python objects.
## Quick example
```python
>>> from pdf4py.parser import Parser
>>> fp = open('tests/pdfs/0000.pdf', 'rb')
>>> parser = Parser(fp)
>>> info_ref = parser.trailer['Info']
>>> print(info_ref)
PDFReference(object_number=114, generation_number=0)
>>> info = parser.parse_reference(info_ref)
>>> print(info)
{'Creator': PDFLiteralString(value=b'PaperCept Conference Management System'),
    ... , 'Producer': PDFLiteralString(value=b'PDFlib+PDI 7.0.3 (Perl 5.8.0/Linux)')}
>>> creator = info['Creator'].value.decode('utf8')
>>> print(creator)
PaperCept Conference Management System
```
