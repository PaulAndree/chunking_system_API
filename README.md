# chunking_system_API


Esta API desarrollada con FastApi busca exponer un endpoint "/process_doc" el cual es capaz de procesar un archivo (pdf, docx, txt) y segmentarlo semanticamente, devolviendo una lista de chunks. Los parametros posibles a configurar para la segmentacion son los siguientes:


El código para esta ingesta se basa fundamentalmente en [MinerU](https://github.com/opendatalab/MinerU) y [semantic-router](https://pypi.org/project/semantic-router/).  
MinerU es una herramienta de código abierto desarrollada por OpenDataLab, diseñada para facilitar el análisis y procesamiento de documentos complejos, como artículos académicos, informes técnicos y libros de texto y llevarlos a formatos estructurados como Markdown y JSON. Sus principales caracteristicas y uso son:

✅ Análisis de diseño avanzado: Utiliza modelos como DocLayout-YOLO para detectar y estructurar elementos del documento, incluyendo encabezados, tablas, texto y fórmulas.

✅ Extracción precisa de contenido: Elimina automáticamente elementos redundantes como encabezados, pies de página y números de página, preservando la coherencia semántica del texto.

✅ Reconocimiento de fórmulas matemáticas: Convierte fórmulas matemáticas en formato LaTeX, facilitando su edición y análisis.

✅ Reconocimiento de tablas: Detecta y extrae tablas, representándolas en formato HTML para su posterior procesamiento

Por otro lado semantic-router es usado para implementar la segmentación semántica de manera automatizada, ya que permite directamente configurar parametros de segmentación.

Ejemplo para llamar a la API:

```python
import requests
url = "http://localhost:8071/process_doc"

response = requests.post(
    url,
    data={"type_name": "note", "content": content, "language": "es"}
)
chunks = response.json()
chunks
```

```python
 # for pdf

import requests
url =  "http://localhost:8071/process_doc"


response = requests.post(
    url,
    files={"file": open( "/home/peyzaguirre/notebooks/dev_chunking_system/table.pdf", "rb")},
    data={"type_name": "pdf","output_dir":"/home/peyzaguirre/notebooks/dev_chunking_system/output", "language":"es"}
)
chunks = response.json()
```

```python
 # for doc
response = requests.post(
    "http://localhost:8071/process_doc",
    files={"file": open( "/home/peyzaguirre/notebooks/dev_chunking_system/Carta.docx", "rb")},
    data={"type_name": "doc","output_dir":"/home/peyzaguirre/notebooks/dev_chunking_system/output", "language":"es"}
)
chunks_doc = response.json()
chunks_doc[0]
```
