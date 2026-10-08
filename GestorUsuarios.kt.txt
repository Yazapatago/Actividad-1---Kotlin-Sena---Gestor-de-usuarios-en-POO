enum class Rol { ADMIN, EDITOR, VISITANTE }
 
interface Autenticable {
    fun autenticar(clave: String): Boolean
}
 
data class Usuario(
    val id: Int,
    val nombre: String,
    val clave: String,
    val rol: Rol
) : Autenticable {
    override fun autenticar(clave: String) = this.clave == clave
}
 
object GestorUsuarios {
    private val usuarios = mutableListOf<Usuario>()
 
    fun agregar(u: Usuario) = usuarios.add(u)
 
    fun validarRol(u: Usuario): String = when (u.rol) {
        Rol.ADMIN -> "${u.nombre}: acceso total"
        Rol.EDITOR -> "${u.nombre}: puede editar contenido"
        Rol.VISITANTE -> "${u.nombre}: solo puede ver contenido"
    }
 
    fun mostrarUsuarios() {
        usuarios.forEach { println(validarRol(it)) }
    }
}
 
fun main() {
    val u1 = Usuario(407, "Tatiana", "Gato#82", Rol.ADMIN)
    val u2 = Usuario(512, "Julián", "Rio2025", Rol.EDITOR)
    val u3 = Usuario(633, "Valeria", "sol*verde", Rol.VISITANTE)

    GestorUsuarios.agregar(u1)
    GestorUsuarios.agregar(u2)
    GestorUsuarios.agregar(u3)

    println("Login Tatiana: ${u1.autenticar("Gato#82")}")
    println("Login Julián: ${u2.autenticar("rio2025")}")

    GestorUsuarios.mostrarUsuarios()
}