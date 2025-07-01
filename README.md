# Principios-Solid
Explicación del principio SOLID grupal.
- S ------> Ariel
- O  -----> Pacha
- L ------> Yesibet
- I ------> Catalina
- D ------> Carolina

SOLID es un conjunto de 5 principios de diseño en la programación orientada a objetos. Su objetivo es ayudarte a escribir código que sea:

📦 Fácil de mantener

🧩 Reutilizable

🛠️ Escalable

🔄 Fácil de testear y modificar sin romper otras partes del sistema

El nombre viene de las iniciales en inglés de cada principio:


✅ S - Principio de responsabilidad única

El Principio de Responsabilidad Única dice que una clase debe hacer una cosa y, por lo tanto, debe tener una sola razón para cambiar.

Para enunciar este principio más técnicamente: Solo un cambio potencial (lógica de base de datos, lógica de registro, etc.) en la especificación del software debería poder afectar la especificación de la clase.

Esto significa que si una clase es un contenedor de datos, como una clase Libro o una clase Estudiante, y tiene algunos campos relacionados con esa entidad, debería cambiar solo cuando cambiamos el modelo de datos.

Es importante seguir el principio de responsabilidad única. En primer lugar, debido a que muchos equipos diferentes pueden trabajar en el mismo proyecto y editar la misma clase por diferentes motivos, esto podría dar lugar a módulos incompatibles.

En segundo lugar, facilita el control de versiones. Por ejemplo, digamos que tenemos una clase de persistencia que maneja las operaciones de la base de datos y vemos un cambio en ese archivo en las confirmaciones de GitHub. Al seguir el PRU, sabremos que está relacionado con el almacenamiento o con cosas relacionadas con la base de datos.

Los conflictos de fusión son otro ejemplo. Aparecen cuando diferentes equipos modifican el mismo archivo. Pero si se sigue el PRU, aparecerán menos conflictos: los archivos tendrán una sola razón para cambiar y los conflictos que existen serán más fáciles de resolver.

✅ O - Principio de apertura y cierre
 El principio de apertura y cierre exige que las clases deban estar abiertas a la extensión y cerradas a la modificación.

Modificación significa cambiar el código de una clase existente y extensión significa agregar una nueva funcionalidad.

Entonces, lo que este principio quiere decir es: Deberíamos poder agregar nuevas funciones sin tocar el código existente para la clase. Esto se debe a que cada vez que modificamos el código existente, corremos el riesgo de crear errores potenciales. Por lo tanto, debemos evitar tocar el código de producción probado y confiable (en su mayoría) si es posible.

Pero, ¿cómo vamos a agregar una nueva funcionalidad sin tocar la clase?, puede preguntarse. Por lo general, se hace con la ayuda de interfaces y clases abstractas.

Ahora que hemos cubierto los conceptos básicos del principio, apliquémoslo a nuestra aplicación Factura.

Digamos que nuestro jefe vino a nosotros y dijo que quiere que las facturas se guarden en una base de datos para que podamos buscarlas fácilmente. Creemos que está bien, esto es fácil jefe, ¡solo dame un segundo!

Creamos la base de datos, nos conectamos a ella y agregamos un método de guardado a nuestra clase FacturaPersistencia:

public class FacturaPersistencia {
Factura factura;

    public FacturaPersistencia(Factura factura) {
        this.factura = factura;
    }

    public void guardarArchivo(String nombreArchivo) {
        // Crea un archivo con el nombre dado y escribe la factura.
    }

    public void guardarEnBaseDatos() {
        // Guarda la factura en la base de datos
    }
}
Lamentablemente, nosotros, como desarrolladores perezosos de la librería, no diseñamos las clases para que fueran fácilmente ampliables en el futuro. Entonces, para agregar esta función, hemos modificado la clase FacturaPersistencia.

Si nuestro diseño de clase obedeciera al principio Abierto-Cerrado, no necesitaríamos cambiar esta clase.

Entonces, como el desarrollador perezoso pero inteligente de la librería, vemos el problema de diseño y decidimos refactorizar el código para obedecer el principio.

interface FacturaPersistencia {

    public void guardar(Factura factura);
}
Cambiamos el tipo de FacturaPersistencia a Interface y agregamos un método de guardado. Cada clase de persistencia implementará este método de guardado.

public class BaseDeDatosPersistencia implements FacturaPersistencia {

    @Override
    public void guardar(Factura factura) {
        // Guardar en la base de datos
    }
}
public class ArchivoPersistencia implements FacturaPersistencia {

    @Override
    public void guardar(Factura factura) {
        // Guardar en archivo
    }
}
Así que nuestra estructura de clases ahora se ve así:

SOLID-Tutorial-1-1024x554
Ahora nuestra lógica de persistencia es fácilmente extensible. Si nuestro jefe nos pide que agreguemos otra base de datos y tengamos 2 tipos diferentes de bases de datos como MySQL y MongoDB, podemos hacerlo fácilmente.

Puede pensar que podríamos simplemente crear múltiples clases sin una interfaz y agregar un método de guardado para todas ellas.

Pero supongamos que ampliamos nuestra aplicación y tenemos varias clases de persistencia como FacturaPersistencia, LibroPersistencia y creamos una clase AdministradorPersistencia que administra todas las clases de persistencia:

public class AdministradorPersistencia {
FacturaPersistencia facturaPersistencia;
LibroPersistencia libroPersistencia;

    public AdministradorPersistencia(FacturaPersistencia facturaPersistencia, LibroPersistencia libroPersistencia) {
        this.facturaPersistencia = facturaPersistencia;
        this.libroPersistencia = libroPersistencia;
    }
}
Ahora podemos pasar cualquier clase que implemente la interfaz FacturaPersistencia a esta clase con la ayuda del polimorfismo. Esta es la flexibilidad que proporcionan las interfaces.

✅ L - Liskov Substitution Principle (LSP)
🧠 Explicación simple: Las clases hijas deben poder reemplazar a la clase madre sin alterar su comportamiento esperado.

🪄 Analogía: Un lapicero con tinta negra reemplaza a uno azul sin cambiar la forma de escribir.

💻 Nuevo ejemplo en Java:

class Empleado {
    public double calcularPago() {
        return 1000.0;
    }
}

class EmpleadoPorHora extends Empleado {
    public double calcularPago() {
        return 20 * 10; // 20 horas * $10
    }
}
➡ Comentario: EmpleadoPorHora puede reemplazar a Empleado y su método funciona correctamente.
✅ I– Interface Segregation Principle (ISP)
✂️ Mejor muchas interfaces pequeñas que una gigante.

❌ Mal diseño:

java
public interface Servicio {
    void pagar();
    void enviarNotificacion();
    void registrarCliente();
}
➡️ ¿Y si una clase solo quiere notificar y no pagar? La estás forzando.

✅ Buen diseño:

java
public interface ServicioPago { void pagar(double monto); }
public interface ServicioNotificacion { void notificar(String mensaje); }
Así solo implementas lo que necesitas.

✅  D – Dependency Inversion Principle (DIP)
🔌 Depende de abstracciones, no de implementaciones.

java
public interface MetodoPago {
    void pagar(double monto);
}

public class PagoConTarjeta implements MetodoPago {
    public void pagar(double monto) {
        System.out.println("Pagando con tarjeta: $" + monto);
    }
}
Y el procesador de pedidos:

java
public class ProcesadorDePedido {
    private MetodoPago metodo;

    public ProcesadorDePedido(MetodoPago metodo) {
        this.metodo = metodo;
    }

    public void procesar(Pedido pedido) {
        double total = new CalculadorTotal().calcular(pedido);
        metodo.pagar(total);
    }
}
➡️ ProcesadorDePedido no sabe si se paga con tarjeta, efectivo o pixie dust. Solo necesita algo que implemente MetodoPago.

RESUMEN

Letra	Principio	Qué significa
S	Single Responsibility Principle	Una clase debe tener una única responsabilidad o motivo de cambio.
O	Open/Closed Principle	El software debe estar abierto a extensión, pero cerrado a modificación.
L	Liskov Substitution Principle	Las clases hijas deben poder reemplazar a sus clases padre sin errores.
I	Interface Segregation Principle	Es mejor tener interfaces específicas que una interfaz gigante.
D	Dependency Inversion Principle	Las clases deben depender de abstracciones, no de implementaciones concretas.
