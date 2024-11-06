# 🚀 Guía de Instalación de Oracle Database con Docker

Bienvenido a esta guía paso a paso para instalar y configurar Oracle Database usando Docker. 🐳

## 📚 Tabla de Contenidos
- [Requisitos Previos](#requisitos-previos)
- [Instalación](#instalación)
- [Configuración](#configuración)
- [Conexión](#conexión)
- [SQL Developer](#sql-developer)
- [Notas Importantes](#notas-importantes)
- [Solución de Problemas Comunes](#solución-de-problemas-comunes)
- [Referencias](#referencias)

---

## 🛠️ Requisitos Previos

### Hardware Recomendado
- **CPU:** Procesador multinúcleo x86-64 (Intel Xeon o AMD EPYC)
- **RAM:** Mínimo 2GB, recomendado 8GB o superior 💻
- **Almacenamiento:** SSD o HDD con espacio suficiente (preferiblemente con RAID) 💾
- **Red:** Conexión de alta velocidad 🌐

### Software Necesario
- **Sistema Operativo:** Windows 10/11, Oracle Linux, Red Hat o similar
- **Docker Desktop:** Debes tener Docker instalado y funcionando 🐳
- **Java Development Kit (JDK) 17:** Requerido para usar SQL Developer ☕️

---

## 📝 Instalación

### 1️⃣ Descarga de la Imagen Oracle
Primero, descarga la imagen oficial de Oracle Database desde el registro de contenedores de Oracle:
```bash
docker pull container-registry.oracle.com/database/free:latest
```

### 2️⃣ Ejecución del Contenedor
Ahora, ejecuta el contenedor con el siguiente comando:
```bash
docker run --name Oracle-db \
-p 1521:1521 \
-p 5500:5500 \
-e ORACLE_CHARACTERSET=utf8 \
-e ENABLE_ARCHIVELOG=true \
-e ORACLE_MEM=4000 \
-e ENABLE_FORCE_LOGGING=true \
-v C:\data\oracle:/opt/oracle/oradata \
-d \
container-registry.oracle.com/database/free:latest
```

### 3️⃣ Verificación del Contenedor
Verifica que el contenedor se esté ejecutando correctamente:
```bash
docker ps
```

---

## ⚙️ Configuración

### Establecer Contraseña de Administrador
Para establecer la contraseña de administrador (por ejemplo, "oracle123"), ejecuta el siguiente comando:
```bash
docker exec Oracle-db ./setPassword.sh <your_password>
```

---

## 🔗 Conexión

### Conexión vía Terminal
Para conectarte a la base de datos a través de SQL*Plus, usa este comando:
```bash
docker exec -it Oracle-db sqlplus sys/<your_password>@FREE as sysdba
```

---

## 💻 SQL Developer

### Instalación de SQL Developer
1. **Descargar SQL Developer** desde el [sitio oficial de Oracle](https://www.oracle.com/database/technologies/appdev/sql-developer.html).
   - **Windows:** Instalar la versión con JDK 17 incluido.
   - **Linux:** Ejecutar el script `sqldeveloper.sh`.

### Configuración de la Conexión
1. **Nombre:** Descripción para la conexión (por ejemplo, "Oracle Docker DB").
2. **Usuario:** `sys` como `sysdba`.
3. **Contraseña:** `<your_password>`.
4. **Host:** `localhost`.
5. **Puerto:** 1521 (o 5500).
6. **Servicio:** `FREE`.

---

## ⚠️ Notas Importantes
- Asegúrate de tener suficientes recursos disponibles antes de iniciar el contenedor. 🔋
- La imagen de Oracle Database FREE es una edición gratuita con limitaciones. 🆓
- Mantén las credenciales en un lugar seguro. 🔐
- Se recomienda realizar copias de seguridad periódicas de la base de datos. 💾

---

## 🛠️ Solución de Problemas Comunes

### Si el contenedor no inicia, verifica los logs:
```bash
docker logs Oracle-db
```

### Para reiniciar el contenedor:
```bash
docker restart Oracle-db
```

---

## 📚 Referencias
- [Documentación Oficial de Oracle Database](https://www.oracle.com/database/)
- [Docker Documentation](https://docs.docker.com/)
