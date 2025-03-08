# Reglas de Codificación en Proyectos

## 1. Convenciones de Nomenclatura

La consistencia en la nomenclatura es fundamental para mantener un código legible y profesional:

- **PascalCase:** Se utiliza para nombres de clases, interfaces y tipos.
`public class ProductController
public interface IProductService
public class UserAuthentication`
- **camelCase:** Se utiliza para nombres de variables, métodos y parámetros.
`private string userId;
public void createProduct(ProductDto product)
boolean isValidUser;`

## 2. Estructura y Organización del Código

Un código bien organizado es más fácil de mantener y entender:

- Separar las funcionalidades en componentes lógicos
- Usar nombres descriptivos que indiquen el propósito
- Mantener los métodos cortos y enfocados en una única responsabilidad

## 3. Ejemplo de Código Spaguetti vs. Código Limpio

**❌ Código Spaguetti (Malo):**

```jsx
function handleProduct(data, type) {
    if(type === 'create') {
        // 100 líneas de lógica mezclada
        validateData(data);
        // más lógica...
        saveToDatabase(data);
        // lógica de envío de emails
        sendEmail(data);
        // actualización de cache
        updateCache();
    } else if(type === 'update') {
        // Similar cantidad de código mezclado
    }
    // Más condiciones...
}

```

**✅ Código Limpio (Bueno):**

```jsx
class ProductService {
    async createProduct(productData) {
        await this.validateProduct(productData);
        const product = await this.saveProduct(productData);
        await this.notifyProductCreation(product);
        return product;
    }

    async updateProduct(id, productData) {
        await this.validateProduct(productData);
        const product = await this.findProduct(id);
        const updatedProduct = await this.saveProduct({...product, ...productData});
        await this.notifyProductUpdate(updatedProduct);
        return updatedProduct;
    }
}

```

## 4. Buenas Prácticas en APIs REST

Ejemplo de estructura clara para endpoints de productos:

```yaml
/api/products:
  post:
    summary: Create new product
    operationId: createProduct
    
  put:
    summary: Update existing product
    operationId: updateProduct
    
  delete:
    summary: Delete product
    operationId: deleteProduct

```

## 5. Recomendaciones Generales

- Escribir código autoexplicativo que requiera mínima documentación
- Implementar pruebas unitarias para cada funcionalidad
- Seguir el principio SOLID para diseño de software
- Realizar revisiones de código regularmente
- Mantener la documentación actualizada

Recuerda: Un código limpio y bien estructurado no solo beneficia al desarrollador actual sino también a futuros mantenedores del proyecto.

## 6. Buenas Prácticas en Frontend

**Estructura y Organización:**

- Organizar componentes por funcionalidad o características
- Mantener una arquitectura consistente (por ejemplo, Atomic Design)
- Implementar lazy loading para optimizar el rendimiento

**Diseño Responsivo:**

- Utilizar unidades relativas (rem, em, %) en lugar de píxeles fijos
- Implementar diseño mobile-first
- Usar media queries de manera estratégica

**Componentes:**

```jsx
// ❌ Componente con responsabilidades mezcladas
const ProductCard = () => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  // Lógica de fetching, manejo de estado y UI mezclados
  useEffect(() => {
    fetchData();
  }, []);

  return (/* ... */);
}

// ✅ Componente limpio con responsabilidades separadas
const ProductCard = ({ product }) => {
  return (
    <Card>
      <ProductImage src={product.image} />
      <ProductInfo {...product} />
      <ActionButtons onAdd={handleAdd} />
    </Card>
  );
}

```

**Estado y Gestión de Datos:**

- Centralizar la gestión del estado (Redux, Context API)
- Implementar manejo de errores consistente
- Utilizar custom hooks para lógica reutilizable

**Rendimiento:**

- Optimizar renders usando React.memo() y useMemo()
- Implementar code splitting para reducir el tamaño del bundle
- Optimizar imágenes y assets

**Accesibilidad:**

- Seguir las pautas WCAG
- Usar elementos semánticos de HTML5
- Implementar navegación por teclado

Recuerda que estas prácticas deben adaptarse según las necesidades específicas del proyecto y el equipo.
