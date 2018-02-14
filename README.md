# Búsqueda BLAST
## Orlandy Ariel Sánchez Acosta.
Búsqueda en la base de datos [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi) médiate la su aplicación web a la cual habrá que proporcionarle una secuencia ATGC, esta buscará en la base de datos según los parámetros que indiquen y se obtendrá un RID, un ID mediante el cual se pueda recuperar la información, y de esta manera poder comprobar si dicha secuencia ATGC se encuentra presente en algún genoma de dicha base.

## Parámetros
El método **construir_peticion** recibe 3 parámetros los cuales están sujeto a condiciones para que se pueda realizar una búsqueda correctamente.

* **Parámetros:**
	* **QUERY:** Consulta de búsqueda, tiene las siguientes opciones de formato:
		* [Accesion](https://support.ncbi.nlm.nih.gov/link/portal/28045/28049/Article/499/What-are-accession-numbers)
		* [GI](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=BlastHelp)
		* [FASTA](https://www.ncbi.nlm.nih.gov/Sitemap/sequenceIDs.html)
    * **DATABASE:** Base de datos de ensamblado de genomas, tiene muchas opciones, para saber cuál elegir mirar el siguiente [enlace (apartado: BLAST Assembled Genomes)](https://nihlibrary.ors.nih.gov/bioinfo/BLAST/Blast.htm), en el podrá consultar todas las bases de datos disponibles.
    	* En el ejemplo de demostración se utiliza nr (Nucleotide Colletion (nr/nt)).
    * **PROGRAM:** Tipo de búsqueda BLAST a utilizar, [ver con más detalles](https://www.ibm.com/support/knowledgecenter/es/SSEPGG_8.2.0/com.ibm.db2.ii.doc/opt/c0007271.htm).
    	* BLASTn
    	> **NOTA:** Uno de los más utilizados generalmente, también se utiliza en el ejemplo.
    	* BLASTp
    	* BLASTx
    	* tBLASTn
    	* tBLASTx

Código de ejemplo de cómo hacer una petición PUT a Blast

```python
import putblast as p

peticionPut = p.PeticionPUTBlast()
cadenaATGC = "GATGACGGTGTCTACATTGTTCCCGACCACTCATCTCCTCTGTCATGCCCGAAACGTCTTCTCAAACCCGTCGT"
peticionPut.construir_peticion(cadenaATGC, "nr","blastn")

peticionPut.realizar_peticion()

print(peticionPut.rid)

```
>**NOTA IMPORTANTE: SI PRETENDE REALIZAR VARIAS PETICIONES SEGUIDAS, SE DEBERÁ DEJAR UN MARGEN MAYOR DE 10 SEGUDNOS PARA EVITAR QUE EL SERVIDOR LO DETECTE COMO ATAQUE, DE LO CONTRARIO NO PERMITIRÁ REALIZAR LAS PETICIONES**

Código de ejemplo de cómo realizar una petición GET a Blast para recuperar el resultado.

``` python

import getblast as p

peticionGet = p.PeticionGETBlast()

peticionGet.construir_peticion("<rid obtenido con el código de ejemplo anterior>")

resultado = peticionGet.realizar_peticion()
print(resultado)
```
> **NOTA:** Se debe tener en cuenta que a la hora de realizar la petición PUT la cadena o query no debe superar los 8000 caracteres, según las pruebas realizadas se puede llegar a un máximo de 8110, pero por seguridad mejor no sobrepasar los 8000 caracteres.

## Librerías utilizadas
* [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
* [URLLib](https://docs.python.org/3/howto/urllib2.html)

