Informe TP final Laboratorio 2

Estructuras:
Además de las estructuras dadas se agrega “datoPalabra” pensado para poder devolver la palabra mas frecuente junto con la cantidad de veces  que esta aparece.

Diccionario:
compararSimbolos(char letra): Compara la letra recibida con una serie de simbolos y retorna 0 si la coincidencia se da o 1 si no.

muestraDiccionario():Muestra el contenido del archivo del diccionario..

deteccionError(char palabra[]): Retorna 0 o 1 de acuerdo a si la palabra recibida es igual o no a la del archivo.

agregarAlDiccionario(termino diccionario[],int* validosD,char archivo[], int validosA, int idDoc): A partir del char archivo y de acuerdo a la posición calculada y al id pasado por parámetro va formando el arreglo de términos que es el diccionario a partir de un archivo de caracteres.

persistenciaDiccionario(termino diccionario[],int validosD): Carga un archivo de terminos seleccionado al diccionario.

cargaString(termino diccionario[], int* validosD, char archivo[], int idDoc): Carga un string con todo el texto del archivo de texto y llama a “agregarAlDiccionario” pasandole sus respectivos parametros.

ultimoIdDoc(): Devuelve el numero de documento de un archivo.

cargaUltIdDoc(int idDoc): Guarda en un archivo el id del ultimo documento que se cargo.

Consulta_Archivo(termino diccionario[], int* validos_d): Funcion para agregar archivos al diccionario (llama a “agregarAlDiccionario”), preguntando al usuario.







Motor de búsqueda:
crearNodoA(char palabra[]): Crea un nuevo nodo de tipo árbol y lo retorna.

crearNodoT(int idDoc,int pos): Lo mismo que el anterior pero con un nodo de tipo termino.

insercionOcurrencia(nodoT**ocurrencias,int idDoc,int pos): Requiere el id y la posición para crear un nuevo nodoT y luego lo inserta de forma ordenada por id creciente.

existeNodo(nodoA* arbol,char dato[]): Requiere el arbol en cuestion y la palabra a buscar. Si encuentra el nodo con la palabra en cuestion lo retorna.

insertarABB(nodoA**arbol,char palabra[],int i, int j): Inserta un nuevo nodoA en el arbol. Es una función recursiva que se maneja con dos variables enteras que funcionan como contadores para ir comparando letra por letra el string de la palabra a insertar y las palabras de los nodoA. Si alguna letra es mayor o menor comparada con la palabra la función va ir a la izquierda o a la derecha respectivamente. La función continua así hasta que no haya ningún nodoA (osea se llegó a una hoja) donde será creado e insertado el nuevo nodo.

minúsculas(char*str): Convierte en minúsculas todas las letras de un string (las funciones tenían problemas para saber cual letra era mayor que otra si había mayusculas).

ordenLexicografico(nodoA**arbol,termino dato): Función que junta a todas las del motor. Recibe un nodo término, lo pasa a minúsculas y después se fija si existe. Si es asi llama a ”insercionOcurrencia” y si no a “insertarABB”.

despersistenciaDiccionario(nodoA** arbol): Recibe el archivo diccionario.bin y mientras tenga archivos en su interior va a llamar a la función anterior.

recorrerLista(nodoA*arbol,nodoT*ocurrenciass): Muestra la palabra del nodo del árbol recibido por parámetro y su lista de ocurrencias.

inorder(nodoA* A): Muestra la palabra del nodo del árbol recibido por parámetro y su frecuencia.





Operaciones de usuario:
Punto 1:
buscarOcurrencia(nodoA* Arbol, char palabra[]): Llama a la función “existeNodo” y si encuentra la palabra muestra (printea), toda su lista de ocurrencias (idDoc y su posicion).

consultaPalabra(nodoA* Arbol): Le pide al usuario que ingrese una palabra a buscar y llama a “buscarOcurrencia”.

Punto 2:
comparacionOcurrencias(nodoA* arbol,char palabra[],int id1, int id2): Función que recibe una palabra y dos id para fijarse que la palabra exista en ambos archivos. Usa “buscarPalabraArbol” para encontrar el nodo y luego va comparando ambos id con los de las ocurrencias.

interseccionArchivos(nodoA* arbol): Menu de operaciones de usuario, le pide al usuario una palabra a buscar y uno o mas archivos donde buscarla.
Punto 3:
lecturaIdMax(): Función que devuelve el id máximo de los archivos (osea la cantidad de archivos en total).

ocurrenciasEnArchivo(nodoT*lista,int id): Muestra todas las ocurrencias de una palabra que coincidan con el id pasado por copia.

busquedasMasTerminosArbol(nodoA* Arbol,char palabra[], int id): busca una palabra en el árbol y si la encuentra llama a la función anterior para mostrar las ocurrencias de acuerdo al id.

busquedasMasTerminos(nodoA* Arbol): Lee la cantidad maxima de archivos. Luego le pregunta al usuario en que archivo quiere buscar la palabra que luego va a ingresar llamando a la función anterior para que la encuentre.

Punto 4:
cmpS(char letra,char letra2): Compara las letras recibidas con simbolos y espacios que puedan terminar una palabra devolviendo 0 si termina y 1 si no.

fromFToW(char word[],char frase[],int*i): Función que devuelve por referencia la cantidad de letras que tiene una frase ademas de cargar otro string con una copia de la frase.

eliminarSimbolosF(char frase[]): Elimina los espacios dobles de la frase pasada por copia.

cantPalabrasFrase(char frase[],int val): Función que cuenta y devuelve la cantidad de palabras que tiene una frase.

compOcurrencias(nodoT*ocurrStr2,int idDoc,int pos): Funcion que  devuelve si encontro  ocurrencias deuna palabra que coincidan con la id y la posición pasadas por copia.

idYPos(nodoT*lista,int*id,int*pos): Le asigna a un id y a una pos pasadas por referencia el id y la pos de la ocurrencia enviada.

especiales(char frase[]): Funcion que llama a “cmpS” y que retorna 0 si encontro un doble espacio o 1 si la palabra esta bien cargada.

buscarFrase(nodoA*arbol): Primero le pide al usuario que ingrese la frase que quiere buscar. Luego llama a “minusculas” y a “eliminarSimbolosF” para preparar la frase y que no ocurran errores. Si la frase tiene dobles espacios le pide al usuario que vuelva a cargarla. Si la cantidad de palabras es menor a 2 busca si existe la palabra en el arbol y si la encuentra lo informa. si son 2 o mas palabras busca si la primera palabra existe en el arbol (si no la busqueda termina ahi), si es asi, tambien busca la segunda y si el id y la pos de alguna ocurrencia de la segunda palabra coincide con la primera mantiene unj flag en 1 y avanza a la siguiente palabra. Si el recorrido de la frase llega a un “\0” y el flag se mantiene en 1 la frase efectivamente se encuentra toda junta en un solo archivo.
Punto 5:
contarOcurrencias(nodoT* lista, int idDoc): Cuenta las ocurrencias de acuerdo al id ingresado.

palabraMasFrecuente(nodoA* arbol, int id): Función recursiva que por medio de dos auxiliares y varias comparaciones devuelve el nodo con la mayor frecuencia de los tres (nodos izquierda, derecha y actual).

consultaMasBuscado(nodoA* arbol): Le pregunta al usuario sobre que archivo quiere saber la palabra mas repetida y llama a la función anterior.
Punto 6:
Coincidencia(nodoA* Arbol, char palabra[]): Si el árbol existe y la función Levenshtein da menor o igual a 3 retorna el nodo actual.

llamadaCoincidencia(nodoA* Arbol): Le pide al usuario que ingrese una palabra y llama a la función anterior.

Levenshtein y mínimo: Provistas por la profe.
