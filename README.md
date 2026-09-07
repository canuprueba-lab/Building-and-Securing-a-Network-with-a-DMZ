<!-- hide -->
# Construyendo y aplicando seguridad a una DMZ

> Por [canu](https://github.com/canuprueba-lab) de [4Geeks Academy](https://4geeksacademy.co/)

<!-- endhide -->

En este laboratori configuraremos diferentes medidas de seguridad a una infraestrucctura entregada

- Aislamiento fundamental para los servicios de la zona desmilitarizada (DMZ)
- Control de trafico listas de acceso
- Coniguracion segura de acceso al servidor web
- Configuracion segura del acceso NAT

## 📝 Procedimiento

1. Inicialmente se configuro la infras estructura existenta con arreglos basicos de configuracion para probar conectividad, segun la sigueinta tabla de direcciones ip:
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/d5e6ae47-0c11-461e-a72b-bfcc1dd20062" />

2. **Configuracion statica del NAT** en el router se configura la NAT para proteger la DMZ desde acceso externo.  
 
3. **Configuracion de ACL (Access Control Lists)** restringimos el trafico entre zonas.  

4. **Realizacion de pruebas de confirmacion de las configuraciones relaizadas**:

<!-- endhide -->
