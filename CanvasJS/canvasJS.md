# O que é o CanvasJS?

<p style="font-size: 12px">fonte: https://canvasjs.com/</p>

CanvasJS é um modo fácil de usar **HTML5** e a **biblioteca gráfica/tabela** do Javascript.

# Integração do JQuery

O CanvasJS permite a utilização de comandos do plugin JQuery. Logo, pode-se utilizar comandos do tipo 
 **$(“selector”).someAction()** para adicionar o gráfico desejado. 
 
      <!DOCTYPE html>
      <html>
      <head>
      <title>CanvasJS Chart jQuery Plugin</title>
      <script type="text/javascript" src="https://canvasjs.com/assets/script/jquery-1.11.1.min.js"></script>  
      <script type="text/javascript" src="https://canvasjs.com/assets/script/jquery.canvasjs.min.js"></script>  
      <script type="text/javascript">
            $(function () {
                  $("#chartContainer").CanvasJSChart({ //Pass chart options
                        data: [
                        {
                        type: "splineArea", //change it to column, spline, line, pie, etc
                        dataPoints: [
                              { x: 10, y: 10 },
                              { x: 20, y: 14 },
                              { x: 30, y: 18 },
                              { x: 40, y: 22 },
                              { x: 50, y: 18 },
                              { x: 60, y: 28 }
                        ]
                  }
                  ]
            });

            });
      </script>
      </head>
      <body>
            <div id="chartContainer" style="width:100%; height:300px;"></div>
      </body>
      </html>

### CanvasJS PHP Charts

Os gráficos/tabelas CanvasJS PHP fornecem renderização animada de forma a tornar os gráficos mais atraentes.
Ainda, eles podem ser executados localmente.

Os **Index Labels ou Data Labels** podem ser usados como informação adicional aos gráficos, tal como o valor no topo dos data points. 

PHP Charts são responsivos e executam em todos os dispositivos (Desktop, Tabletes e dispositivos móveis).

### Adicionando CanvasJS à suas Web Pages

Inclua o arquivo canvasjs.min.js dentro da web page.

    <head>
      <script type="text/javascript" src="canvasjs.min.js"></script>
    </head>

### Customização relacionada

A propriedade **indexLabelPlacement** é utilizado para mudar a localização dos Index / Data Labels.
As propriedades **indexLabelFontSize** e **indexLabelFontColor** são utilizados para mudar o tamanho da fonte e sua cor.
Outras propriedades usadas incluem **indexLabelFontFamily, indexLabelBackgroundColor,** etc.

### PHP Drilldown Charts & Graphs

A funcionalidade **Drilldown** é usada para explorar de forma mais detalhada, revelando detalhes adicionais.



