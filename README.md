# fluentd-custom

Revisar documentacion de la pila ELK para levantar el contendor de elasticsearch y kibana.

**Guardar los archivos en un directorio.** 

El log que se planea tomar como fuente se ubicaria en un directorio del host /var/log/logsforfluentd/httpd-access.log y comparte volumen con el contenedor con /var/log/httpd-access.log

**Construir la imagen ubicado en el mismo directorio.**
docker build -t custom-fluentd:latest ./

**levantar el contenedor** 
docker run -p 10514:10514/udp -p 24224:24224/udp -p 24220:24220 -v /var/log/logsforfluentd/httpd-access.log:/var/log/httpd-access.log:z -v $(pwd)/log:/fluentd/log --name custom-ctin custom-fluentd:latest 

