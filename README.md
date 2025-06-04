Trabajo Práctico – Base de Datos II (1C - Noche)
Equipo 03

Descripción
Este repositorio contiene el Script para la generacion de la base de datos para el práctico de la materia Base de Datos II correspondiente al primer cuatrimestre (turno noche).

Objetivo
Desarrollar un sistema que permita gestionar de forma integral el proceso de alquiler de canchas, aplicando conceptos clave como el diseño de modelos entidad-relación, consultas SQL, procedimientos almacenados, triggers y vistas, garantizando la integridad y eficiencia en el manejo de datos.

Integrantes
Martin, Matias – 29822

Garcia, Tomás Ezequiel – 29780

Minafra, Matias – 29830

Explicación del Sistema
El sistema desarrollado permite: Gestión de usuarios y roles, aeserva de canchas, administración de horarios disponibles, gestión de canchas y tipos, control de sucursales y localidades, promociones y descuentos.
La base de datos incluye tres vistas, dos procedimientos almacenados y dos triggers, automatizando tareas clave y asegurando la consistencia de los datos. También se desarrolló el Diagrama Entidad-Relación (DER) con todas las tablas y campos definidos.


-----------------------------------------------------------------
SCRIPT PARA CREAR LA BASE DE DATOS
------------------------------------------------------------------

CREATE DATABASE Canchas_BD2;

CREATE TABLE Localidad (
    id_localidad INT IDENTITY (1,1) NOT NULL PRIMARY KEY,
    Nombre VARCHAR(50) NOT NULL
);

CREATE TABLE Sucursal (
    id_sucursal INT IDENTITY (1,1) NOT NULL PRIMARY KEY,
    id_localidad INT NOT NULL FOREIGN KEY REFERENCES Localidad (id_localidad),
    Nombre VARCHAR (50),
    Telefono VARCHAR (20),
    Mail VARCHAR (50)
);    

CREATE TABLE Estados (
    id_estado INT IDENTITY (1,1) NOT NULL PRIMARY KEY,
    Descripcion VARCHAR (50) NOT NULL
);

CREATE TABLE Roles (
    id_rol INT IDENTITY (1,1) NOT NULL PRIMARY KEY,
    Nombre_Rol VARCHAR(50) NOT NULL
);

CREATE TABLE Usuarios (
    id_usuario INT IDENTITY (1,1) NOT NULL PRIMARY KEY,
    id_rol INT NOT NULL FOREIGN KEY REFERENCES Roles (id_rol),
    id_estado INT NOT NULL FOREIGN KEY REFERENCES Estados (id_estado),
    Nombre VARCHAR (50),
    Apellido VARCHAR (50),
    Direccion VARCHAR (50),
    CUIT CHAR(20),
    Telefono CHAR(10),
    Contraseña VARCHAR (20), //Podemos poner un CHECK para que sea minimo 8 max 12
    Fecha_Alta DATATIME
);
CREATE TABLE Reservas (
    id_reserva INT NOT NULL PRIMARY KEY IDENTITY (1,1),
    id_usuario INT NOT NULL FOREIGN KEY REFERENCES Usuarios(id_usuario),
    id_cancha INT FOREIGN KEY REFERENCES Canchas(id_cancha),
    id_estado INT NOT NULL FOREIGN KEY REFERENCES Estados(id_estado),
    hora_f DATETIME,
    hora_inicio DATETIME NOT NULL,
    fecha_reserva DATETIME DEFAULT GETDATE(),
    monto_total MONEY
);
CREATE TABLE Canchas (
    id_cancha INT NOT NULL PRIMARY KEY IDENTITY (1,1),
    id_estado INT NOT NULL FOREIGN KEY REFERENCES Estados(id_estado),
    id_tipo_cancha INT NOT NULL FOREIGN KEY REFERENCES Tipos_Cancha(id_tipo_cancha),
    id_sucursal INT NOT NULL FOREIGN KEY REFERENCES Sucursales(id_sucursal),
    nombre VARCHAR(50) NOT NULL,
    iluminacion BIT NOT NULL CHECK (iluminacion IN (0, 1)), -- 0: Sin iluminación, 1: Con iluminación
    techada BIT NOT NULL CHECK (techada IN (0, 1)) -- 0: No techada, 1: Techada
);
CREATE TABLE Horarios_Disponibles (
    id_horario_dispo INT NOT NULL PRIMARY KEY IDENTITY (1,1),
    id_cancha INT NOT NULL FOREIGN KEY REFERENCES Canchas(id_cancha),
    id_estado INT NOT NULL FOREIGN KEY REFERENCES Estados(id_estado),
    hora_inicio DATETIME NOT NULL,
    hora_fin DATETIME NOT NULL CHECK (hora_fin > hora_inicio),
    dia_semana INT NOT NULL CHECK (dia_semana BETWEEN 0 AND 6) -- 0 = Domingo, 6 = Sábado
);


