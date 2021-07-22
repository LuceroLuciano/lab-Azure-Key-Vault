# lab-Azure-Key-Vault
## Administración de una contraseña en Azure Key Vault
[Azure Key Vault](https://docs.microsoft.com/es-mx/learn/modules/protect-against-security-threats-azure/4-manage-secrets-key-vault) es un servicio de la nube de Azure centralizado para almacenar secretos, claves de cifrado y certificados SSL/TLS de la aplicación en una unica ubicación central.

### Ejercicio:
En este ejercicio se agrega una contraseña a Azure Key Vault. Una contraaseña es un ejemplo de información confidencial que se debe proteger. Luego se lee la contraseña desde Azure Key Vault para comprobrar que es accesible.<br><br> Puede usar [Azure Portal](https://docs.microsoft.com/es-mx/learn/modules/management-fundamentals/2-identify-product-options), la [CLI de Azure](https://docs.microsoft.com/es-mx/learn/modules/management-fundamentals/2-identify-product-options) o [Azure PowerShell](https://docs.microsoft.com/es-mx/learn/modules/management-fundamentals/2-identify-product-options). En este caso crea un secreto en Key Vault mediante Azure Portal. Luego se accede al secreto desde el portal y desde la CLI de Azure en Azure Cloud Shell.

### Creación de un Almacén de claves
1. Vaya a [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com)<br>
2. En el menú de Azure Portal o en la página de **Inicio**, seleccione **Crear un recurso**.
3. En la barra de búsqueda, escriba **Almacén de claves** y, depues, seleccione **Almacén de claves**.
4. En el panel **Almacén de claves**, seleccione **Crear**. Aparecera el panel para **crear el almacén de claves**.
5. En la pestalla **Datos básicos**, rellene los valores siguientes para cada parametro.<br><br>
DETALLES DEL PROYECTO <br>
Suscripción = **Suscripción que Concierne**<br>
Grupo de recursos = **Nombre del grupo de recursos del espacio aislado**<br><br>
DETALLES DE INSTANCIA<br>
Nombre del almacén de claves = **my-keyvault-NNN**<br>
Deje las otras opciones de configuración con sus valores predeterminados><br>
![Almacén de claves](https://github.com/LuceroLuciano/lab-Azure-Key-Vault/blob/main/imagens/almacen%20de%20claves%201.JPG)

#### NOTA: Remplace **NNN** por una serie de números. Esto ayuda a garantizar que el nombre del almacen de claves sea único.<br>

6. Seleccione **Revisar y crear** y, una vez superada a validación, seleccione **Crear**.<br> Espere a que la implmentación se complete correctamente.<br>
![Crear almacen de claves](https://github.com/LuceroLuciano/lab-Azure-Key-Vault/blob/main/imagens/almacen%20de%20claves%202.JPG)

7. Haga click en  **Go to resource** (ir al recurso).
8. Observe algunos detalles sobre almacén de claves.<br>Por ejemplo, en el campo **Vault URI** (URI del almacén) de muestra el URI que puede usar la aplicacón para acceder al almacén desde la API de REST.<br> Este es un ejemplo de un almacén de claves denominado **my-Keyvaul20071998:**<br>  ![Información esencial](https://github.com/LuceroLuciano/lab-Azure-Key-Vault/blob/main/imagens/almacen%20de%20claves%203.JPG) 
9. Como paso opcional, puede examinar algunas de as otras caracteristicas en **Configuración**, en el panel de menús de la izquierda.<br>Aunque iicialmente estan vacías, aquí encontrará ubicaciones donde puede almacenar claves, secretos y certificados. 

### Adición de una contraseña el almacén de claves.
1. En el panel de menús de la izquierda, en **Configuración**, seleccione **Secretos**. Aparecerá el panel de almacén de claves.
2. En la barra de menús superior, seleccione **Generar/Importar**. Aparecerá el panel para crear un secreto.
3. Rellene los siguientes valores para cada configuación. <br>
Opciones de carga = **Manual** <br>
Nombre = **MyPassword**<br>
Value = **hVFKK96** <br> 
Deje las otras opciones de configuración con sus valores predeterminados. Tenga en cuenta que puede especificar propiedades como la fecha de activacón y la de expiración. También puede deshabilitar el acceso al secreto. 
4. Seleccione **Crear**
![Crear un secreto](https://github.com/LuceroLuciano/lab-Azure-Key-Vault/blob/main/imagens/crear%20un%20secreto%201.JPG)

### Mostrar la contraseña
Aquí se accede a la contraseña del almacen de claves dos veces. En primer lugar se accede desde Azure Portal. luego se accede desde la CLI de Azure.
  1. En el panel **Almacén de claves/Secretos**, seleccione **MyPassword**. Aparecerá el panel **MyPassword/Versiones**. Se ve que la versión actual esta habilitada. ![MyPassword](https://github.com/LuceroLuciano/lab-Azure-Key-Vault/blob/main/imagens/crear%20un%20secreto%202.JPG)
  2. Seleccione la versión actual. Aparecerá el panel **Versión del secreto**.<br>En **identificador secreto** se ve un URI que ahora puede usar con las aplicaciones para acceder al secreto. Recuere que solo las aplicaiones autorizadas pueden acceder  a este secreto. <br> 
3. Selecciones **Mostrar valor secreto** <br> ![Versión del secreto](https://github.com/LuceroLuciano/lab-Azure-Key-Vault/blob/main/imagens/crear%20un%20secreto%203.JPG) <br> ![Valor secreto](https://github.com/LuceroLuciano/lab-Azure-Key-Vault/blob/main/imagens/crear%20un%20secreto%204.JPG)
  4. Ejecute este comando en Cloud Shell
  ```
  az keyvault secret show \
  --name MyPassword \
  --vault-name <my-keyvault-NNN> \
  --query value \
  --output tsv
  ```
  #### NOTA: Remplace **>my-keyvault-NNN<** por el nombre que usó anteriormente
  5. Verá la contraseña en la salida. <br>
  ![Secreto mostrado en la CLI de Azure](https://github.com/LuceroLuciano/lab-Azure-Key-Vault/blob/main/imagens/comando%20para%20mostrar%20el%20secreto.JPG)
  
<br>En este punto, tiene un almacén de claves que contiene un secreto de contraseñas que se almacenan de forma segura para su uso con las aplicaciones. 
  

