from typing import List, Dict
import unittest

# Función que muestra productos en pantalla (retorna lista de strings para test)
def mostrar_productos(productos: List[Dict]) -> List[str]:
    if not productos:
        return []
    resultado = []
    for p in productos:
        # Mostramos solo productos en stock (puedes cambiar según necesidad)
        if p.get("in_stock", False):
            texto = f"{p['name']} - {p['description']} - {p['price']} {p['currency']}"
            resultado.append(texto)
    return resultado


# Datos de ejemplo (podrían venir del JSON)
productos_ejemplo = [
    {
        "id": 1,
        "name": "iPhone 13",
        "description": "The latest iPhone from Apple",
        "price": 999.99,
        "currency": "USD",
        "in_stock": True
    },
    {
        "id": 2,
        "name": "Samsung Galaxy S21",
        "description": "The latest Samsung phone",
        "price": 899.99,
        "currency": "USD",
        "in_stock": True
    },
    {
        "id": 3,
        "name": "Google Pixel 6",
        "description": "The latest Google phone",
        "price": 799.99,
        "currency": "USD",
        "in_stock": False
    }
]


# Pruebas unitarias
class TestMostrarProductos(unittest.TestCase):

    def test_mostrar_productos_con_datos(self):
        salida = mostrar_productos(productos_ejemplo)
        self.assertTrue(len(salida) > 0)
        self.assertIn("iPhone 13 - The latest iPhone from Apple - 999.99 USD", salida)
        self.assertIn("Samsung Galaxy S21 - The latest Samsung phone - 899.99 USD", salida)
        # Google Pixel no debería aparecer porque no está en stock
        self.assertNotIn("Google Pixel 6 - The latest Google phone - 799.99 USD", salida)

    def test_mostrar_productos_lista_vacia(self):
        salida = mostrar_productos([])
        self.assertEqual(len(salida), 0)


if __name__ == "__main__":
    unittest.main()
