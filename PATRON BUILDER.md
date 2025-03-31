# PATRON BUILDER
## Tipo de patrón: CREACIONAL

### Introducción
El patrón Builder es un patrón de diseño creacional cuyo objetivo es separar la construcción de un objeto complejo de su representación final. Esto permite que el mismo proceso de construcción pueda crear diferentes representaciones del objeto. En el contexto del desarrollo de software, el patrón Builder se utiliza para evitar constructores con múltiples parámetros y para simplificar la creación de objetos compuestos, lo que facilita el mantenimiento y la escalabilidad del código.

### ¿Por qué utilizar el patrón Builder?
- **Claridad en la construcción:** Al dividir el proceso de construcción en pasos independientes, el código se vuelve más legible y fácil de mantener.
- **Flexibilidad:** Permite crear diferentes tipos de objetos a partir de la misma secuencia de construcción, adaptándose a distintas necesidades sin alterar la lógica del cliente.
- **Evita constructores complejos:** Elimina la necesidad de tener constructores con múltiples parámetros, lo cual reduce errores y mejora la comprensión del código.
- **Facilita la extensión:** Al separar la lógica de construcción, es más sencillo añadir nuevas características o componentes al objeto sin modificar el proceso global.

# Ventajas

- **Modularidad:**  
  Al encapsular cada paso de la construcción, se facilita la reutilización y el aislamiento de cambios.

- **Separación de responsabilidades:**  
  El director se encarga de la secuencia de construcción mientras que los builders concretos se centran en la creación de componentes específicos.

- **Personalización:**  
  Es posible crear variaciones del producto final sin afectar la lógica general del proceso de construcción.

# Desventajas

- **Complejidad:**  
  Puede introducir una capa adicional de abstracción, lo que en casos simples podría ser innecesario.

- **Mayor cantidad de clases:**  
  La implementación del patrón puede aumentar el número de clases en el sistema, lo que podría complicar la estructura del proyecto si no se gestiona adecuadamente.

# Consideraciones de implementación

- **Inmutabilidad del producto:**  
  Una vez construido el objeto, es recomendable que éste sea inmutable para evitar inconsistencias.

- **Fluidez en la construcción:**  
  Algunos lenguajes permiten utilizar una interfaz fluida (fluent interface) para hacer que la secuencia de construcción sea más legible y encadenada.

# Patrones Relacionados

- **Abstract Factory:**  
- **Factory Method:**  
- **Prototype:**  

# Fuentes (Formato APA)

- Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley.
- Freeman, E., Freeman, E., Bates, B., & Sierra, K. (2004). *Head First Design Patterns*. O'Reilly Media.


### Ejemplo de aplicación real
Imagina que estamos desarrollando una aplicación que genera informes financieros. Estos informes pueden requerir diferentes formatos (por ejemplo, PDF, HTML o Excel) y cada uno de ellos consta de secciones como encabezado, cuerpo, gráficos y pie de página. Utilizando el patrón Builder, se puede definir una estructura común para la creación del informe y luego implementar constructores específicos para cada formato.

### Ejemplo en Pseudocódigo

```pseudo
// Definición de la interfaz Builder
interface ReportBuilder {
    method buildHeader()
    method buildBody()
    method buildGraphs()
    method buildFooter()
    method getReport() : Report
}

// Implementación concreta para construir un informe en PDF
class PDFReportBuilder implements ReportBuilder {
    private report: Report

    method buildHeader() {
        report.add("Encabezado del informe en PDF")
    }

    method buildBody() {
        report.add("Cuerpo del informe con datos financieros")
    }

    method buildGraphs() {
        report.add("Gráficos financieros en formato PDF")
    }

    method buildFooter() {
        report.add("Pie de página con notas legales")
    }

    method getReport() : Report {
        return report
    }
}

// Director que orquesta la construcción del informe
class ReportDirector {
    private builder: ReportBuilder

    method setBuilder(builder: ReportBuilder) {
        this.builder = builder
    }

    method constructReport() {
        builder.buildHeader()
        builder.buildBody()
        builder.buildGraphs()
        builder.buildFooter()
    }
}

// Uso del patrón en el código cliente
director = new ReportDirector()
builder = new PDFReportBuilder()
director.setBuilder(builder)
director.constructReport()
pdfReport = builder.getReport()

![image](https://github.com/user-attachments/assets/8616102b-2692-41d3-8905-7db59686ee0c)


