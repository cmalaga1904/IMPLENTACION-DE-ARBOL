#include <iostream>
#include <cstdlib>
using namespace std;

struct nodo {
    int valor;
    int altura;
    struct nodo *izq, *der;
};

struct nodo *raiz, *aux, *aux2;

int altura(struct nodo *n) {
    return (n == NULL) ? 0 : n->altura;
}

int balance(struct nodo *n) {
    return (n == NULL) ? 0 : altura(n->izq) - altura(n->der);
}

struct nodo* rotarDerecha(struct nodo *y) {
    struct nodo *x = y->izq;
    struct nodo *T2 = x->der;

    x->der = y;
    y->izq = T2;

    y->altura = max(altura(y->izq), altura(y->der)) + 1;
    x->altura = max(altura(x->izq), altura(x->der)) + 1;

    return x;
}

struct nodo* rotarIzquierda(struct nodo *x) {
    struct nodo *y = x->der;
    struct nodo *T2 = y->izq;

    y->izq = x;
    x->der = T2;

    x->altura = max(altura(x->izq), altura(x->der)) + 1;
    y->altura = max(altura(y->izq), altura(y->der)) + 1;

    return y;
}

void insertar(int valor) {
    if (raiz == NULL) {
        raiz = (struct nodo*)malloc(sizeof(struct nodo));
        raiz->valor = valor;
        raiz->altura = 1;
        raiz->izq = raiz->der = NULL;
        return;
    }

    aux = raiz;
    while (aux != NULL) {
        aux2 = aux;
        if (valor < aux->valor) {
            aux = aux->izq;
        } else if (valor > aux->valor) {
            aux = aux->der;
        } else {
            return;
        }
    }

    struct nodo *nuevo = (struct nodo*)malloc(sizeof(struct nodo));
    nuevo->valor = valor;
    nuevo->altura = 1;
    nuevo->izq = nuevo->der = NULL;

    if (valor < aux2->valor) {
        aux2->izq = nuevo;
    } else {
        aux2->der = nuevo;
    }
}

void eliminar(int valor) {
    aux = raiz;
    aux2 = NULL;

    while (aux != NULL && aux->valor != valor) {
        aux2 = aux;
        if (valor < aux->valor) {
            aux = aux->izq;
        } else {
            aux = aux->der;
        }
    }

    if (aux == NULL) return;

    if (aux->izq == NULL && aux->der == NULL) {
        if (aux == raiz) {
            raiz = NULL;
        } else if (aux2->izq == aux) {
            aux2->izq = NULL;
        } else {
            aux2->der = NULL;
        }
        free(aux);
    } else if (aux->izq == NULL || aux->der == NULL) {
        struct nodo *hijo = (aux->izq != NULL) ? aux->izq : aux->der;
        if (aux == raiz) {
            raiz = hijo;
        } else if (aux2->izq == aux) {
            aux2->izq = hijo;
        } else {
            aux2->der = hijo;
        }
        free(aux);
    } else {
        struct nodo *sucesor = aux->der;
        while (sucesor->izq != NULL) {
            sucesor = sucesor->izq;
        }
        int valorSucesor = sucesor->valor;
        eliminar(sucesor->valor);
        aux->valor = valorSucesor;
    }
}

void mostrar(struct nodo *actual, int nivel) {
    if (actual != NULL) {
        mostrar(actual->der, nivel + 1);
        cout << string(nivel * 4, ' ') << actual->valor << endl;
        mostrar(actual->izq, nivel + 1);
    }
}

int main() {
    int opcion, valor;

    do {
        cout << "\n1. Insertar";
        cout << "\n2. Mostrar";
        cout << "\n3. Eliminar";
        cout << "\n4. Salir";
        cout << "\n\nOpcion: ";
        cin >> opcion;

        switch (opcion) {
            case 1:
                cout << "Valor a insertar: ";
                cin >> valor;
                insertar(valor);
                break;

            case 2:
                mostrar(raiz, 0);
                break;

            case 3:
                cout << "Valor a eliminar: ";
                cin >> valor;
                eliminar(valor);
                break;

            case 4:
                cout << "Saliendo del programa." << endl;
                break;

            default:
                cout << "Opcion no valida." << endl;
                break;
        }

    } while (opcion != 4);

    return 0;
}
