# listas c++
aca hay algunas funciones de listas simples, circulares.

# definiendo el nodo:

<pre>
struct Nodo {
    int dato;
    Nodo *siguiente;
    }
</pre>

luego en la funcion main, agregaremos un puntero, el cual apuntara a NULL, gracias a ello, vamos a poder saber donde comienza la lista.

una vez echo esto, vamos a proceder con las funciones de cada lista:

# lista simplemente enlazada:
estas listas solo tienen una direccion de enlazado.

### insertar elementos al inicio:
<pre>
    void insertar_lista(Nodo *& lista, int n){
        Nodo *nuevo_nodo = new Nodo();  // con esto, creamos el nodo nuevo.
        nuevo_nodo -> dato = n;         // igualamos el dato del nuevo nodo con el entero n que le asignamos a la funcion
        nuevo_nodo -> siguiente = lista ; //igualamos el puntero (hacia donde apuntara este nodo).
        lista = nuevo_nodo;             // le decimos a lista que el ultimo nodo es el que creamos recien.
    }
</pre>
cada parametro de la lista, debe coincidir con los datos del struct creado como nodo.

### insertar elementos al final:
<pre>
    void insertar_final(Nodo *& lista, int n){
        Nodo *nuevo_nodo = new Nodo();
        nuevo_nodo -> dato = n;
        nuevo_nodo -> siguiente = NULL; // este nuevo_nodo, como apunta al ultimo lugar de la lista, sera nulo.

         if(lista == NULL){ // si lista es NULL, iguala lista al nodo.
            lista = nuevo_nodo;
    
         }else{
            Nodo *temp = lista;
            while(temp -> siguiente != NULL){ // busca el nodo nulo
                temp = temp -> siguiente;
            }
        }
        temp -> siguiente = nuevo_nodo; // cuando encuentra el nodo, hace que apunte al nuevo nodo que es nulo
    }

</pre>

### insertar un elemento en lugar especifico:

<pre>
    void insertarespecifico(Nodo *& lista, int n, int indice){
        if(indice = 0){
            insertar_lista(lista, n);
        }else{
            int count = 0;
            Nodo *temp = lista;
            while(temp != NULL && count < indice - 1){
                count ++;
                temp = temp -> siguiente;
            }
            
            if(temp != NULL){
                Nodo *nuevo_nodo = new Nodo();
                nuevo_nodo -> dato = n;
                nuevo_nodo -> siguiente = temp -> siguiente;
                temp -> siguiente = nuevo_nodo;
            } // si se encuentra el indice, pero no es nulo, se acomod ael nodo en el indice indicado para que indique la posicion siguiente del "(indice -1)" y el nodo en "(indice -1)" se enlaza al nuevo nodo.
        }
            
    }
</pre>

### eliminacion de un elemento al incio:

<pre>
    void eliminar_primer_nodo(Nodo *&lista){
        if(lista != NULL){ // si la lista no esta vacia.
            Nodo *temp = lista; // crea un nodo temp
            lista = lista -> siguiente; // mueve el puntero del primer nodo hacia el segundo.
            delete temp; // elimina el nodo.
        }
    }
</pre>

### eliminar un elemento especifico:

<pre>
    void eliminar_especifico(Nodo *& lista, int n){
        Nodo *anterior = NULL;
        Nodo *actual = lista;

        while(actual != NULL && actual -> dato != n){ // recorremos la lista hasta encontrar el numero
            anterior = actual;
            actual = actual -> siguiente;
        } 
        if(actual != NULL){ 
            if(anterior != null){ // se actualiza el nodo para "saltar" el que sera eliminado.
                anterior -> siguiente = actual -> siguiente; 
            }
        }else{
            lista = actual -> siguiente; // actualiza lista ppara el cambio de nodos
        }
        delete actual; //se borra el nodo actual (el nodo especifico)
    }
</pre>

### buscar un valor en la lista:
<pre>
    bool buscar_valor(Nodo *& lista, int n){
        Nodo *temp = lista;
        while(temp != NULL){
            if (temp -> dato == n){
                return true; // retorna verdadero si encuentra el nodo 
            }
        temp = temp -> siguiente; // avanza al siguiente nodo.
        }
        return false; // si no encuentra el nodo con ese valor, retornara falso.
    }
</pre>

### recorrer e imprimir la lista:

<pre>
    void imprimir_lista(Nodo *& lista){
        Nodo *temp = lista;
        while(temp != NULL){
            cout << temp -> dato << " -> ";
            temp = temp -> siguiente;
        }
        cout << endl;
    }
</pre>

# bueno, ahora agrego un par de funciones de listas circulares.

### agregar al principio de la lista circular:

<pre>
    void insertar_al_principio(Nodo*& lista, int n) {
        Nodo* nuevo_nodo = new Nodo();
        nuevo_nodo->dato = n;
    
        // Si la lista no está vacía, encontrar el último nodo y actualizar su puntero siguiente
            if (lista != nullptr) {
                Nodo* ultimo = lista;
                while (ultimo->siguiente != lista) {
                ultimo = ultimo->siguiente;
            }
                ultimo->siguiente = nuevo_nodo;
            } else {
            // Si la lista está vacía, hacer que el nuevo nodo apunte a sí mismo
        nuevo_nodo->siguiente = nuevo_nodo;
        }

    nuevo_nodo->siguiente = lista;
    lista = nuevo_nodo;
    }
</pre>

### agregar al final de la lista:

<pre>
    void insertar_al_final(Nodo*& lista, int n) {
        Nodo* nuevo_nodo = new Nodo();
        nuevo_nodo->dato = n;

        // Si la lista está vacía, hacer que el nuevo nodo apunte a sí mismo
           if (lista == nullptr) {
                nuevo_nodo->siguiente = nuevo_nodo;
                lista = nuevo_nodo;
            } else {
            // Encontrar el último nodo y actualizar su puntero siguiente
                Nodo* ultimo = lista;
                while (ultimo->siguiente != lista) {
                ultimo = ultimo->siguiente;
            }
        ultimo->siguiente = nuevo_nodo;
        nuevo_nodo->siguiente = lista;
        }
    }
</pre>

### buscar una posicion:

<pre>
    int buscar_posicion(Nodo* lista, int posicion) {
            if (lista == nullptr || posicion < 0) {
            // Puedes manejar el error de alguna manera, o simplemente devolver un valor predeterminado
            return -1; // Otra opción podría ser lanzar una excepción en lugar de devolver un valor especial
            }

            Nodo* actual = lista;
            int contador = 0;

        do {
            if (contador == posicion) {
                // Devolver el valor del nodo encontrado
                return actual->dato;
            }

            actual = actual->siguiente;
            contador++;
        } while (actual != lista);

        // Si la posición no se encontró en la lista, podrías devolver un valor predeterminado o manejarlo de alguna otra manera
        return -1; // Otra opción podría ser lanzar una excepción en lugar de devolver un valor especial
    }
</pre>

### insertar en una posicion especifica:

<pre>
    void insertar_en_posicion(Nodo*& lista, int n, int posicion) {
       Nodo* nuevo_nodo = new Nodo();
        nuevo_nodo->dato = n;

        if (posicion == 0) {
            insertar_al_principio(lista, n);
            return;
        }

        Nodo* anterior = buscar_posicion(lista, posicion - 1);

        if (anterior == nullptr) {
            cout << "La posición no es válida." << endl;
            delete nuevo_nodo;
            return;
        }

        nuevo_nodo->siguiente = anterior->siguiente;
        anterior->siguiente = nuevo_nodo;
    }
</pre>

### mostrar lista circular:

<pre>
    void mostrar_lista(Nodo* lista) {
       if (lista == nullptr) {
            cout << "La lista está vacía." << endl;
            return;
        }

        Nodo* actual = lista;

        do {
            cout << actual->dato << " ";
            actual = actual->siguiente;
        } while (actual != lista);

        cout << endl;
    }
</pre>

### recorrer lista por un valor especifico:

<pre>
    bool recorrer_lista(Nodo *& lista, std::string charla) {
      if (lista == nullptr) {
        return false; // La lista está vacía, no hay nada que recorrer
      }

      Nodo *temp = lista;
      do {
        if (temp->charla == charla) {
        return true;
        }
        temp = temp->siguiente;
      } while (temp != lista);

      return false;
    }
</pre>

### eliminar un valor especifico de la lista.
<pre>
    void eliminar_nodo(Nodo*& lista, int dato_a_eliminar) {
    if (lista == nullptr) {
        cout << "La lista está vacía. No se puede eliminar el nodo." << endl;
        return;
    }

    Nodo* actual = lista;
    Nodo* anterior = nullptr;

    do {
        if (actual->dato == dato_a_eliminar) {
            if (actual == lista) {
                if (actual->siguiente == lista) {
                    delete actual;
                    lista = nullptr;
                } else {
                    Nodo* ultimo = lista;
                    while (ultimo->siguiente != lista) {
                        ultimo = ultimo->siguiente;
                    }
                    ultimo->siguiente = actual->siguiente;
                    lista = actual->siguiente;
                    delete actual;
                }
            } else {
                anterior->siguiente = actual->siguiente;
                delete actual;
            }

            cout << "Nodo con el dato " << dato_a_eliminar << " eliminado exitosamente." << endl;
            return;
        }

        anterior = actual;
        actual = actual->siguiente;
    } while (actual != lista);

    cout << "El dato no se encuentra en la lista." << endl;
}

</pre>

# si hay alguna que falte, manden...

# @nachoodubra 2023

