# Modelos originales de Deep Learning para el Reconocimiento de Terreno en Marte (AI4MARS)

Ahora en esta sección detallaremos la selección de arquitecturas para la segmentación semántica de las imagenes, y nuestra linea de pensamiento detras de porque el seria un buen modelo para nuestro proyecto, incluyendo un paper que lo respalde

## Tabla de Modelos y Papers de Referencia

| Modelo | Paper Original | Referencia (Link) | ¿Por qué funcionaría en este proyecto? |
| :--- | :--- | :--- | :--- |
| **PSANet** | Point-wise Spatial Attention Network for Scene Parsing (Zhao et al., ECCV 2018) | [Ver Paper](https://openaccess.thecvf.com/content_ECCV_2018/html/Hengshuang_Zhao_PSANet_Point-wise_Spatial_ECCV_2018_paper.html) | Su mecanismo de atención "punto a punto" ayuda a capturar relaciones de larga distancia entre texturas similares, ideal para distinguir vastas zonas de arena. |
| **UPerNet** | Unified Perceptual Parsing for Scene Understanding (Xiao et al., ECCV 2018) | [Ver Paper](https://openaccess.thecvf.com/content_ECCV_2018/html/Tete_Xiao_Unified_Perceptual_Parsing_ECCV_2018_paper.html) | Al unificar información de múltiples escalas, permite identificar desde pequeños guijarros hasta grandes afloramientos rocosos de forma simultánea. |
| **BiSeNetV2** | BiSeNet V2: Bilateral Network with Guided Aggregation (Yu et al., IJCV 2021) | [Ver Paper](https://link.springer.com/article/10.1007/s11263-021-01437-3) | Equilibra la extracción de detalles espaciales con el contexto semántico, ofreciendo alta precisión en los bordes de las rocas sin sacrificar velocidad. |
| **Fast-SCNN** | Fast-SCNN: Fast Semantic Segmentation Network (Poudel et al., arXiv 2019) | [Ver Paper](https://arxiv.org/abs/1902.04502) | Diseñado para tiempo real en hardware limitado; es perfecto para simular la inferencia en el hardware real de un rover (recursos computacionales bajos). |
| **SegFormer** | SegFormer: Simple and Efficient Design for Semantic Segmentation with Transformers (Xie et al., NeurIPS 2021) | [Ver Paper](https://arxiv.org/abs/2105.15203) | Este utiliza Transformers para capturar texturas globales de Marte de forma eficiente, superando a las CNNs tradicionales en robustez ante cambios de iluminación. |

---

## Notas Adicionales de Implementación

> **El desafío del color:** En Marte, el desafío principal es la **baja varianza visual** (predominancia de tonos rojizos y marrones).

* **Contexto vs. Detalle:** Modelos como **PSANet** y **UPerNet** son robustos en este entorno porque analizan la imagen de forma global para entender qué es suelo y qué es roca basándose en la continuidad del entorno, no solo en el color del píxel.
* **Eficiencia Energética y de Hardware:** A la hora de pensar en el enfoque de implementacion del modelo para un desplazamiento en el rover en tiempo real, **BiSeNetV2** y **Fast-SCNN** son nuestros mejores aliados debido a su arquitectura de doble rama que permite procesar imágenes de alta resolución con baja latencia.
* **Robustez de SegFormer:** Al no usar *positional encodings* fijos, este modelo se adapta mejor a diferentes resoluciones de entrada, algo común cuando se trabaja con cámaras de distintos rovers, y lo cual es importante tambien el considerar.