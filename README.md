# Principios-Solid
Explicación del principio SOLID grupal.
- S ------> Ariel
- O  -----> Pacha
- L ------> Yesibet

✅ S - Principio de responsabilidad única

El Principio de Responsabilidad Única dice que una clase debe hacer una cosa y, por lo tanto, debe tener una sola razón para cambiar.

Para enunciar este principio más técnicamente: Solo un cambio potencial (lógica de base de datos, lógica de registro, etc.) en la especificación del software debería poder afectar la especificación de la clase.

Esto significa que si una clase es un contenedor de datos, como una clase Libro o una clase Estudiante, y tiene algunos campos relacionados con esa entidad, debería cambiar solo cuando cambiamos el modelo de datos.

Es importante seguir el principio de responsabilidad única. En primer lugar, debido a que muchos equipos diferentes pueden trabajar en el mismo proyecto y editar la misma clase por diferentes motivos, esto podría dar lugar a módulos incompatibles.

En segundo lugar, facilita el control de versiones. Por ejemplo, digamos que tenemos una clase de persistencia que maneja las operaciones de la base de datos y vemos un cambio en ese archivo en las confirmaciones de GitHub. Al seguir el PRU, sabremos que está relacionado con el almacenamiento o con cosas relacionadas con la base de datos.

Los conflictos de fusión son otro ejemplo. Aparecen cuando diferentes equipos modifican el mismo archivo. Pero si se sigue el PRU, aparecerán menos conflictos: los archivos tendrán una sola razón para cambiar y los conflictos que existen serán más fáciles de resolver.

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


- I ------> Catalina
- D ------> Carolina

SOLID es un conjunto de 5 principios de diseño en la programación orientada a objetos. Su objetivo es ayudarte a escribir código que sea:

📦 Fácil de mantener

🧩 Reutilizable

🛠️ Escalable

🔄 Fácil de testear y modificar sin romper otras partes del sistema

El nombre viene de las iniciales en inglés de cada principio:
