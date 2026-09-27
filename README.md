1. CREAR BASE DE DATOS
   
CREATE DATEBASE Venta_tech;

Sección 1 — DROP TABLES
 
DROP TABLE IF EXISTS ventas,
DROP TABLE IF EXISTS productos,
DROP TABLE IF EXISTS clientes;
DROP TABLE IF EXISTS categorias;

Sección 2 — CREATE TABLES
TABLA CATEGORIAS

CREATE TABLE Categorias (
id_categoria INT NOT NULL,
nombre_categoria NVARCHAR (50) NOT NULL,
descripcion NVARCHAR(200) NULL,
CONSTRAINT PK_categorias PRIMARY KEY (id_categoria)
);

TABLA CLIENTES
CREATE TABLE Clientes (
id_cliente INT NOT NULL,
nombre NVARCHAR (100) NOT NULL,
email NVARCHAR (100) NULL,
ciudad NVARCHAR (50) NULL,
fecha_registro DATE NOT NULL,
CONSTRAINT PK_clientes PRIMARY KEY (id_cliente),
CONSTRAINT UQ_cliente_email UNIQUE (email)
);

TABLA PRODUCTOS
CREATE TABLE Productos (
id_producto INT NOT NULL,
nombre_producto NVARCHAR (100) NOT NULL,
id_categoria INT NOT NULL,
precio DECIMAL (10,2) NOT NULL,
stock INT NOT NULL DEFAULT 0,
activo BIT NOT NULL DEFAULT 1,
CONSTRAINT PK_productos PRIMARY KEY (id_producto),
CONSTRAINT FK_productos_categorias FOREIGN KEY (id_categoria)
REFERENCES categorias (id_categoria)
);

TABLA VENTAS
CREATE TABLE Ventas (
id_venta INT NOT NULL,
id_cliente INT NOT NULL,
id_producto INT NOT NULL,
cantidad INT NOT NULL,
precio_unitario DECIMAL (10,2) NOT NULL,
fecha_venta DATE NOT NULL,
CONSTRAINT PK_venta PRIMARY KEY (id_venta),
CONSTRAINT FK_ventas_clientes  FOREIGN KEY (id_cliente)
REFERENCES clientes (id_cliente),
CONSTRAINT FK_ventas_productos FOREIGN KEY (id_producto)
REFERENCES productos (id_producto)
);

Sección 3 — INSERT DATA
 REGISTRO - CATEGORIAS
INSERT INTO categorias (id_categoria, nombre_categoria, descripcion) VALUES
    (1, N'Computación',    N'Laptops, PCs y monitores'),
    (2, N'Accesorios',     N'Periféricos y complementos'),
    (3, N'Audio',          N'Auriculares y parlantes'),
    (4, N'Almacenamiento', N'Discos y memorias');

   REGISTRO CLIENTES
  INSERT INTO clientes (id_cliente, nombre, email, ciudad, fecha_registro) VALUES
    (1, N'María López',  N'maria@mail.com',  N'Buenos Aires', '2024-01-05'),
    (2, N'Carlos Ruiz',  N'carlos@mail.com', N'Córdoba',      '2024-01-10'),
    (3, N'Ana Gómez',    N'ana@mail.com',    N'Rosario',      '2024-02-01'),
    (4, N'Pedro Sanz',   N'pedro@mail.com',  N'Mendoza',      '2024-02-15'),
    (5, N'Laura Torres', N'laura@mail.com',  N'Tucumán',      '2024-03-01');

   REGISTRO PRODUCTOS
  INSERT INTO productos (id_producto, nombre_producto, id_categoria, precio, stock, activo) VALUES
    (1, N'Laptop Pro 15',      1, 1200.00, 15, 1),
    (2, N'Mouse Inalámbrico',  2,   28.00, 80, 1),
    (3, N'Monitor 4K 27"',     1,  450.00, 12, 1),
    (4, N'Auriculares BT Pro', 3,  120.00, 35, 1),
    (5, N'SSD Externo 1TB',    4,  130.00, 18, 1),
    (6, N'Teclado Mecánico',   2,   95.00, 40, 1);

   REGISTRO VENTAS
   INSERT INTO ventas (id_venta, id_cliente, id_producto, cantidad, precio_unitario, fecha_venta) VALUES
    ( 1, 1, 1, 2, 1200.00, '2024-03-05'),
    ( 2, 2, 2, 5,   28.00, '2024-03-06'),
    ( 3, 3, 3, 1,  450.00, '2024-03-07'),
    ( 4, 1, 4, 2,  120.00, '2024-03-08'),
    ( 5, 4, 5, 3,  130.00, '2024-03-10'),
    ( 6, 2, 6, 4,   95.00, '2024-03-11'),
    ( 7, 5, 1, 1, 1200.00, '2024-03-12'),
    ( 8, 3, 2, 8,   28.00, '2024-03-13'),
    ( 9, 4, 4, 1,  120.00, '2024-03-14'),
    (10, 5, 3, 2,  450.00, '2024-03-15');

Sección 4 — VALIDACIÓN
SELECT *
FROM categorias; confirmado 4 filas

SELECT *
FROM clientes; confirmado 5 filas

SELECT *
FROM productos; confirmado 6 filas

SELECT *
FROM ventas; confirmado 10 filas







