Trabajo Práctico – Base de Datos II (1C - Noche)
Equipo 03

Descripción
Este repositorio contiene el trabajo práctico de la materia Base de Datos II correspondiente al primer cuatrimestre (turno noche). El proyecto consiste en el diseño e implementación de un sistema de reservas para canchas deportivas, construido sobre una base de datos relacional.

Objetivo
Desarrollar un sistema que permita gestionar de forma integral el proceso de alquiler de canchas, aplicando conceptos clave como el diseño de modelos entidad-relación, consultas SQL, procedimientos almacenados, triggers y vistas, garantizando la integridad y eficiencia en el manejo de datos.

Integrantes
Martin, Matias – 29822

Garcia, Tomás Ezequiel – 29780

Minafra, Matias – 29830

Explicación del Sistema
El sistema desarrollado permite:
Gestión de usuarios y roles.
Reserva de canchas.
Administración de horarios disponibles.
Gestión de canchas y tipos.
Control de sucursales y localidades.
Promociones y descuentos.
La base de datos incluye tres vistas, dos procedimientos almacenados y dos triggers, automatizando tareas clave y asegurando la consistencia de los datos. También se desarrolló el Diagrama Entidad-Relación (DER) con todas las tablas y campos definidos.

-----------------------------------------------------------------
SCRIPT PARA CREAR LA BASE DE DATOS
------------------------------------------------------------------

CREATE DATABASE Canchas_BD2;

CREATE TABLE Localidad(
 id_localidad INT NOT NULL PRIMARY KEY, 
 Nombre VARCHAR (100) NOT NULL
);
 
