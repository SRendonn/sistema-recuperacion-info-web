# Sistemas de Recuperación de Información Web: Taller 1

* Nombre: Sebastián Rendón Giraldo
* Cédula: 1000755047

## Ejercicio 1

```xml
<?xml version="1.0" encoding="UTF-8"?> <!-- El prólogo XML, define la versión y el encoding -->
<!--SISTEMAS DE RECUPERACION WEB--> <!-- Se realizan comentarios con "<!\-\- ## CONTENIDO ## \-\->" -->
<libros xmlns="https://books.org"> <!-- Este es el root del documento. El atributo xmlns define un namespace, un prefijo para los hijos de este elemento -->
    <libro ISBN="1613820917"> <!-- Se pueden definir atributos para un elemento, en este caso el ISBN, deben ir entre comillas dobles o simples -->
        <titulo>Hamlet</titulo>
        <autor>W. Shakespeare</autor>
        <paginas>330</paginas>
        <editorial>Simon &amp; Brown</editorial> <!-- Las entidades XML que sirven para denotar caracteres especiales o no nativos a XML: &amp; &lt; &gt; &quot; &nbsp; -->
    </libro>
    <libro ISBN="9789584254726">
        <titulo>La sombra del viento</titulo>
        <autor>Carlos Ruiz Safron</autor>
        <paginas>575</paginas>
        <editorial>Planeta Booket</editorial>
    </libro>
    <libro ISBN="0765367297">
        <titulo>&lt; Halo &gt; The Fall of Reach</titulo><!-- Entidades especiales &lt; &gt; -->
        <autor>Eric Nylund</autor>
        <paginas>448</paginas>
        <editorial>Tor Books</editorial>
    </libro>
</libros>
```

## Ejercicio 2

### Versión con errores

```xml
<?xml version="\1.0">
<--Sistemas de Recuperacion-->
<mensaje>
<remite.>
nombre id=8976>Alfredo Reino</nombre>
<email>alf@ibium.com</email>
</remite>
<destinatario>>
<nommbre>>
<nombre id=0976>Bill Clinton</nombre>
<email>>president@whitehouse.gov
</destinatario/>
<asunto">Hola Bill</asunto>
<texto.>
<[CDATA[
<mensaje> trabajo de clase <>
ejemplos
]
<<parrafo>¿Hola qué tal? Hace <enfasis->mucho</enfasis> que no escribes. A ver si llamas
y quedamos para tomar algo.</parrafo>
</texto>
</mensaje>
</mensaje>
```

### Versión corregida

```xml
<?xml version="1.0"?>
<!-- Version "\1.0" es inválida, debe ser "1.0". Falta "?" final -->
<!--Sistemas de Recuperacion-->
<!-- Falta el "!" al inicio para que sea un comentario -->
<mensaje>
    <remite>
        <!-- tags no coinciden, renombrarla -->
        <nombre id="8976">Alfredo Reino</nombre> <!-- Falta tag nombre inicial, atributo id debe estar entre comillas -->
        <email>alf@ibium.com</email>
    </remite>
    <destinatario>
        <!-- &gt; innecesario, removerlo -->
        <!-- &gt; innecesario, removerlo, tag sin cierre, removerlo o cerrarlo -->
        <nombre id="0976">Bill Clinton</nombre> <!-- Atributo id debe estar entre comillas -->
        <email>president@whitehouse.gov</email> <!-- &gt; innecesario, removerlo, tag sin cierre, cerrarlo -->
    </destinatario> <!-- tag de cierre con un backslash innecesario, removerlo -->
    <asunto>Hola Bill</asunto> <!-- Comilla innecesaria, typo, removerla -->
    <texto>
        <!-- tags no coinciden, renombrarla -->
        <![CDATA[
<mensaje> trabajo de clase <>
ejemplos
]]>
        <!-- CDATA mal abierto, falta "!" inicial. CDATA mal cerrado, cambiar "]" por "]]>" -->
        <parrafo>
            ¿Hola qué tal? Hace
            <enfasis>mucho</enfasis>
            que no escribes. A ver si llamas <!-- &lt; innecesario al inicio del tag parrafo, eliminarlo. Tag enfasis no coincide, renombrarlo -->
            y quedamos para tomar algo.
        </parrafo>
    </texto>
</mensaje><!-- tag mensaje de cierre innecesario, ya se cerró arriba, eliminarlo -->
```

## Ejercicio 3

```xml
<?xml version="1.0" encoding="UTF-8"?>

<legos xmlns="https://www.lego.com">
    <lego id="42083" height="14.76in" width="22.44in" depth="5.91in">
        <name>LEGO Technic Bugatti Chiron</name>
        <price currency="USD">349.99</price>
        <pieces>3599</pieces>
    </lego>
    <lego id="42123" height="4.5in" width="12in" depth="4in">
        <name>LEGO Technic McLaren Senna GTR</name>
        <price currency="USD">49.99</price>
        <pieces>830</pieces>
    </lego>
    <lego id="42125" height="14.76in" width="22.44in" depth="5.91in">
        <name>LEGO Technic Ferrari 488 GTE "AF Corse #51"</name>
        <price currency="USD">169.99</price>
        <pieces>1677</pieces>
    </lego>
</legos>
```

## Ejercicio 4

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mc:micasa xmlns:mc='http://www.geneura.org/micasa' xmlns:mueble='http://www.geneura.org/mueble'>
    <mc:habitacion id="comedor">
        <mc:mueble>
            <mueble:nombre>Sofá</mueble:nombre>
            <mueble:descripcion>Peludo</mueble:descripcion>
        </mc:mueble>
    </mc:habitacion>
</mc:micasa>
```

## Ejercicio 5

### Versión principal

Con un elemento hijos que contiene los hijos de la persona.

```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="familia">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="persona" minOccurs="4" maxOccurs="4">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="nombre" type="xs:string" />
                            <xs:element name="apellido" type="xs:string" />
                            <xs:element name="edad">
                                <xs:simpleType>
                                    <xs:restriction base="xs:nonNegativeInteger">
                                      <xs:maxInclusive value="120" />
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:element>
                            <xs:element name="hijos">
                                <xs:complexType>
                                    <xs:sequence>
                                        <xs:element name="hijo" minOccurs="2" maxOccurs="unbounded">
                                            <xs:complexType>
                                                <xs:choice>
                                                    <xs:element name="nombre" type="xs:string" />
                                                    <xs:element name="edad">
                                                        <xs:simpleType>
                                                            <xs:restriction base="xs:nonNegativeInteger">
                                                                <xs:maxInclusive value="120" />
                                                            </xs:restriction>
                                                        </xs:simpleType>
                                                    </xs:element>
                                                </xs:choice>
                                            </xs:complexType>
                                        </xs:element>
                                    </xs:sequence>  
                                </xs:complexType>
                            </xs:element>
                            <xs:element name="mes-nacimiento">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:enumeration value="enero" />
                                        <xs:enumeration value="febrero" />
                                        <xs:enumeration value="marzo" />
                                        <xs:enumeration value="abril" />
                                        <xs:enumeration value="mayo" />
                                        <xs:enumeration value="junio" />
                                        <xs:enumeration value="julio" />
                                        <xs:enumeration value="agosto" />
                                        <xs:enumeration value="septiembre" />
                                        <xs:enumeration value="octubre" />
                                        <xs:enumeration value="noviembre" />
                                        <xs:enumeration value="diciembre" />
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:element>
                        </xs:sequence>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

### Versión alternativa

Sin agrupar los hijos dentro de un elemento hijos.

```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="familia">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="persona" minOccurs="4" maxOccurs="4">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="nombre" type="xs:string" />
                            <xs:element name="apellido" type="xs:string" />
                            <xs:element name="edad">
                                <xs:simpleType>
                                    <xs:restriction base="xs:nonNegativeInteger">
                                      <xs:maxInclusive value="120" />
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:element>
                            <xs:element name="hijo" minOccurs="2" maxOccurs="unbounded">
                                <xs:complexType>
                                    <xs:choice>
                                        <xs:element name="nombre" type="xs:string" />
                                        <xs:element name="edad">
                                            <xs:simpleType>
                                                <xs:restriction base="xs:nonNegativeInteger">
                                                    <xs:maxInclusive value="120" />
                                                </xs:restriction>
                                            </xs:simpleType>
                                        </xs:element>
                                    </xs:choice>
                                </xs:complexType>
                            </xs:element>
                            <xs:element name="mes-nacimiento">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:enumeration value="enero" />
                                        <xs:enumeration value="febrero" />
                                        <xs:enumeration value="marzo" />
                                        <xs:enumeration value="abril" />
                                        <xs:enumeration value="mayo" />
                                        <xs:enumeration value="junio" />
                                        <xs:enumeration value="julio" />
                                        <xs:enumeration value="agosto" />
                                        <xs:enumeration value="septiembre" />
                                        <xs:enumeration value="octubre" />
                                        <xs:enumeration value="noviembre" />
                                        <xs:enumeration value="diciembre" />
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:element>
                        </xs:sequence>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema> 
```

## Ejercicio 6

Generado a partir del esquema de la versión principal.

```xml
<?xml-model href="ejercicio5.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<familia>
  <persona>
    <nombre>Sebastian</nombre>
    <apellido>Rendon</apellido>
    <edad>21</edad>
    <hijos>
      <hijo>
        <nombre>Hasan el gato</nombre>
      </hijo>
      <hijo>
        <nombre>Mi PC</nombre>
      </hijo>
    </hijos>
    <mes-nacimiento>mayo</mes-nacimiento>
  </persona>
  <persona>
    <nombre>Santiago</nombre>
    <apellido>Rendon</apellido>
    <edad>21</edad>
    <hijos>
      <hijo>
        <edad>1</edad>
      </hijo>
      <hijo>
        <nombre>El PC de él</nombre>
      </hijo>
    </hijos>
    <mes-nacimiento>mayo</mes-nacimiento>
  </persona>
  <persona>
    <nombre>Gildardo</nombre>
    <apellido>Rendón</apellido>
    <edad>59</edad>
    <hijos>
      <hijo>
        <edad>21</edad>
      </hijo>
      <hijo>
        <nombre>Santiago</nombre>
      </hijo>
      <hijo>
        <edad>35</edad>
      </hijo>
      <hijo>
        <nombre>Andrea</nombre>
      </hijo>
    </hijos>
    <mes-nacimiento>julio</mes-nacimiento>
  </persona>
  <persona>
    <nombre>Teresita</nombre>
    <apellido>Giraldo</apellido>
    <edad>54</edad>
    <hijos>
      <hijo>
        <nombre>Sebastian</nombre>
      </hijo>
      <hijo>
        <nombre>Santiago</nombre>
      </hijo>
    </hijos>
    <mes-nacimiento>marzo</mes-nacimiento>
  </persona>
</familia>
```
