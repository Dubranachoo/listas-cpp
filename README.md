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
    Nodo *nuevo_nodo = new Nodo(); // con esto, creamos el nodo nuevo.
    nuevo_nodo -> dato = n; // igualamos el dato del nuevo nodo con el entero n que le asignamos a la funcion
    nuevo_nodo -> siguiente = lista ; //igualamos el puntero (hacia donde apuntara este nodo).
    lista = nuevo_nodo; // le decimos a lista que el ultimo nodo es el que creamos recien.
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







