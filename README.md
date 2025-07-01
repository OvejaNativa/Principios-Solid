# Principios-Solid
Explicación del principio SOLID grupal.
- S ------> Ariel
- O  -----> Pacha
- L ------> Yesibet


✅ L - Liskov Substitution Principle (LSP)
🧠 Explicación simple: Las clases hijas deben poder reemplazar a la clase madre sin alterar su comportamiento esperado.

🪄 Analogía: Un lapicero con tinta negra reemplaza a uno azul sin cambiar la forma de escribir.

💻 Nuevo ejemplo en Java:

java
Copiar
Editar
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
