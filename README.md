# Búsqueda BLAST

Búsqueda en la base de datos [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi) médiate la su aplicación web a la cual habrá que proporcionarle una secuencia ATGC, esta buscará en la base de datos según los parámetros que indiquen y se obtendrá un RID, un ID mediante el cual se pueda recuperar la información, y de esta manera poder comprobar si dicha secuencia ATGC se encuentra presente en algún genoma de dicha base.

Código de ejemplo de cómo hacer una petición PUT a Blast

```python
import PeticionPUTBlast as p

peticionPut = p.PeticionPUTBlast()
cadenaATGC = "GATGACGGTGTCTACATTGTTCCCGACCACTCATCTCCTCTGTCATGCCCGAAACGTCTTCTCAAACCCGTCGT"
peticionPut.construir_peticion("blastn&MEGABLAST=on","nr",cadenaATGC)

rid = peticionPut.realizar_peticion()

print(rid)

```