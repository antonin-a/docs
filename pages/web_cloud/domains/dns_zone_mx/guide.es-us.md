---
title: 'Añadir un registro MX a la configuración del dominio'
excerpt: 'Cómo añadir un registro MX a la configuración de un dominio en OVHcloud'
updated: 2023-08-30
---

> [!primary]
> Esta traducción ha sido generada de forma automática por nuestro partner SYSTRAN. En algunos casos puede contener términos imprecisos, como en las etiquetas de los botones o los detalles técnicos. En caso de duda, le recomendamos que consulte la versión inglesa o francesa de la guía. Si quiere ayudarnos a mejorar esta traducción, por favor, utilice el botón «Contribuir» de esta página.
>

## Objetivo

El registro MX permite asociar un dominio al servidor de su plataforma de correo. Es indispensable para que el servicio de correo electrónico del remitente pueda llegar al del destinatario.

**Esta guía explica cómo configurar un registro MX para un dominio en OVHcloud.**

## Requisitos

- Tener acceso a la gestión de la zona DNS del dominio desde el [área de cliente de OVHcloud](https://ca.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/world/&ovhSubsidiary=ws).
- Haber iniciado sesión en el [área de cliente de OVHcloud](https://ca.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/world/&ovhSubsidiary=ws).
- El dominio debe utilizar la configuración de OVHcloud (es decir, los servidores DNS de OVHcloud).
- Tener una solución MX Plan (incluida en el plan de [alojamiento web](https://www.ovhcloud.com/es/web-hosting/)), [Exchange](https://www.ovhcloud.com/es/emails/), o un servicio de correo externo.

> [!primary]
>
> - Si el dominio no utiliza los servidores DNS de OVHcloud, deberá editar los registros MX desde el panel que le ofrezca el proveedor que gestione la configuración del dominio.
>
> - Si el dominio está registrado en OVHcloud, compruebe que utiliza nuestra configuración en el [área de cliente](https://ca.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/world/&ovhSubsidiary=ws) de OVHcloud. En la pestaña « `Servidores DNS`{.action} » de la columna izquierda, haga clic en Dominios en la columna izquierda y seleccione el dominio correspondiente, en la pestaña `Información General`{.action}. Si en la sección "**Servidores DNS**" aparece el epígrafe `Activo`, usted utiliza los servidores DNS de OVHcloud.
>
> ![Correo electrónico](images/email-dns-conf-mx00.png){.thumbnail}

## Procedimiento

### Comprender la función de los registros MX 

Los registros MX (**M**ail **e**Xchange) permiten asociar su dominio a los servidores de correo de recepción asociados al servicio de correo. Vamos a basarnos en un ejemplo.

Cuando la dirección **sender@otherdomain.ovh** envía un correo electrónico a **contact@mydomain.ovh**, el servidor de envío de correo (**Outgoing mail server**) envía el siguiente mensaje:

- **(1)** consultar la zona DNS del dominio **mydomain.ovh** y leer los registros **MX**.
- **(2)** reenviar el mensaje de correo electrónico a la URL del registro **MX** leído.

![Correo electrónico](images/email-dns-conf-mx01-ca.png){.thumbnail}

El mensaje se enviará al destino **mx0.mail.ovh.ca**, precedido del valor **0**. Este valor se denomina prioridad. El valor más bajo se consulta primero y el más alto después. Esto significa que la presencia de varios registros permite paliar la falta de respuesta del registro MX de menor prioridad.

Puede configurar varios registros MX para un mismo dominio. Es necesario definir un número de prioridad para cada uno de ellos. Los registros MX se consultan en orden ascendente, desde el número más bajo hasta el más alto, hasta que el servidor receptor responde.

> [!warning]
>
> En general, **modificar los registros MX en la zona DNS de un dominio es una operación delicada**: una manipulación incorrecta puede hacer imposible recibir mensajes de correo en sus direcciones. Preste especial atención al realizar esta operación.
> En caso de duda, le recomendamos que contacte con un [proveedor especializado](https://partner.ovhcloud.com/es/directory/).

### Valores de la configuración MX de OVHcloud <a name="mxovhcloud"></a>

A continuación ofrecemos la configuración MX de OVHcloud que deberá utilizar para nuestros MX Plan (incluido en un plan de [hosting de OVHcloud](https://www.ovhcloud.com/es/web-hosting/)) y [Exchange](https://www.ovhcloud.com/es/emails/). Nuestros servidores de correo disponen de antispam y antivirus integrado.

|Dominio|TTL|Registro|Prioridad|Destino|
|---|---|---|---|---|
|*Dejar el campo vacío*|3600|MX|1|mx0.mail.ovh.ca.|
|*Dejar el campo vacío*|3600|MX|5|mx1.mail.ovh.ca.|
|*Dejar el campo vacío*|3600|MX|50|mx2.mail.ovh.ca.|
|*Dejar el campo vacío*|3600|MX|100|mx3.mail.ovh.ca.|
|*Dejar el campo vacío*|3600|MX|200|mx4.mail.ovh.ca.|

Estos registros MX deben estar configurados en la zona DNS del dominio.

### Configurar un registro MX en una zona DNS de OVHcloud

Para crear o modificar los registros MX en la configuración de su dominio en OVHcloud, conéctese al [área de cliente de OVHcloud](https://ca.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/world/&ovhSubsidiary=ws). Acceda a la sección `Nombres de dominio`{.action}, haga clic en el dominio correspondiente y, seguidamente, abra la pestaña `Zona DNS`{.action}.

Esta tabla muestra la configuración de OVHcloud del dominio. Cada línea corresponde a un registro DNS.

En primer lugar, compruebe que los registros MX ya existen en la configuración DNS de OVHcloud de su dominio utilizando la lista de filtros que aparece sobre la tabla de su zona DNS.<br>
Seleccione el tipo **MX** y acepte para ver solo los registros DNS MX de su zona DNS. Consulte la captura de pantalla a continuación.

![Registro MX en la zona DNS](images/mx-records-dns-zone.png){.thumbnail}

- Si los registros MX ya existen y desea modificarlos, haga clic en el botón `...`{.action} a la derecha de cada fila de la tabla correspondiente y seleccione `Modificar el registro`{.action}.
- Si no hay ningún registro MX, haga clic en el botón `Añadir un registro`{.action} a la derecha de la tabla y seleccione `MX`{.action}. Introduzca la información solicitada en función de la solución de correo elegida:

**Si tiene contratada una solución de correo electrónico de OVHcloud**, consulte la información que encontrará en el apartado [Conocer la configuración MX de OVHcloud](#mxovhcloud).

![Registro MX en la zona DNS](images/mx-records-dns-zone-modif.png){.thumbnail}

Una vez que haya introducido toda la información, siga los pasos que se indican y haga clic en `Aceptar`{.action}.

**Si dispone de otra solución de correo**, consulte la información que le haya proporcionado su proveedor de servicios de correo.

> [!primary]
>
> Los cambios tardan entre 4 y 24 horas en propagarse y ser efectivos.
>

## Más información

[Información general sobre los servidores DNS](/pages/web_cloud/domains/dns_server_general_information)

[Editar una zona DNS de OVHcloud](/pages/web_cloud/domains/dns_zone_edit)

[Configurar un registro SPF en un dominio](/pages/web_cloud/domains/dns_zone_spf)

[Configurar un registro DKIM](/pages/web_cloud/domains/dns_zone_dkim)

Para servicios especializados (posicionamiento web, desarrollo...), póngase en contacto con los [partners de OVHcloud](https://partner.ovhcloud.com/es/).

Si necesita ayuda sobre el uso y la configuración de sus soluciones de OVHcloud, puede consultar nuestras diferentes [ofertas de soporte](https://www.ovhcloud.com/es/support-levels/).

Interactúe con nuestra comunidad de usuarios en <https://community.ovh.com/en/>.
