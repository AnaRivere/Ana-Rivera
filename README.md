# Ana-Rivera
SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
-- -----------------------------------------------------
-- Schema dbproyectofinal
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema dbproyectofinal
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `dbproyectofinal` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci ;
USE `dbproyectofinal` ;

-- -----------------------------------------------------
-- Table `dbproyectofinal`.`tclientes`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `dbproyectofinal`.`tclientes` (
  `idCliente` VARCHAR(15) NOT NULL,
  `Nombre` VARCHAR(50) NOT NULL,
  `Apellido` VARCHAR(50) NOT NULL,
  `Telefono` VARCHAR(30) NOT NULL,
  `Direccion` VARCHAR(80) NOT NULL,
  PRIMARY KEY (`idCliente`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `dbproyectofinal`.`tempresa`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `dbproyectofinal`.`tempresa` (
  `idEmpresa` INT NOT NULL,
  `Nombre` VARCHAR(80) NOT NULL,
  `Direccion` VARCHAR(100) NOT NULL,
  `Telefono` VARCHAR(30) NOT NULL,
  `Email` VARCHAR(80) NOT NULL,
  `RTN` VARCHAR(45) NOT NULL,
  `Fax` VARCHAR(50) NOT NULL,
  `Rubro` VARCHAR(45) NOT NULL,
  `Slogan` VARCHAR(100) NOT NULL,
  `Logo` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`idEmpresa`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `dbproyectofinal`.`tplatillos`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `dbproyectofinal`.`tplatillos` (
  `idPlatillo` VARCHAR(15) NOT NULL,
  `Nombre` VARCHAR(50) NOT NULL,
  `Precio` INT NOT NULL,
  `TipoPlatillo` VARCHAR(45) NOT NULL,
  `Descripcion` VARCHAR(200) NOT NULL,
  PRIMARY KEY (`idPlatillo`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `dbproyectofinal`.`tpedidodomicilio`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `dbproyectofinal`.`tpedidodomicilio` (
  `idPedidoD` INT NOT NULL AUTO_INCREMENT,
  `idClienteD` VARCHAR(15) NOT NULL,
  `NombreClienteD` VARCHAR(50) NOT NULL,
  `TelefonoD` VARCHAR(15) NOT NULL,
  `DireccionD` VARCHAR(80) NOT NULL,
  `idPlatilloD` VARCHAR(15) NOT NULL,
  `NombrePlatilloD` VARCHAR(50) NOT NULL,
  `PrecioD` INT NOT NULL,
  `DescripcionD` VARCHAR(200) NOT NULL,
  `CantidadD` INT NOT NULL,
  `FechaD` VARCHAR(15) NOT NULL,
  PRIMARY KEY (`idPedidoD`),
  INDEX `fkPedidoDomicilioCliente_idx` (`idClienteD` ASC) VISIBLE,
  INDEX `fkPedidoDomicilioPlatillo_idx` (`idPlatilloD` ASC) VISIBLE,
  CONSTRAINT `fkPedidoDomicilioCliente`
    FOREIGN KEY (`idClienteD`)
    REFERENCES `dbproyectofinal`.`tclientes` (`idCliente`),
  CONSTRAINT `fkPedidoDomicilioPlatillo`
    FOREIGN KEY (`idPlatilloD`)
    REFERENCES `dbproyectofinal`.`tplatillos` (`idPlatillo`))
ENGINE = InnoDB
AUTO_INCREMENT = 5
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `dbproyectofinal`.`tpedidorestaurante`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `dbproyectofinal`.`tpedidorestaurante` (
  `idPedidoR` INT NOT NULL AUTO_INCREMENT,
  `idClienteR` VARCHAR(15) NOT NULL,
  `NombreClienteR` VARCHAR(50) NOT NULL,
  `TelefonoR` VARCHAR(45) NOT NULL,
  `idPlatilloR` VARCHAR(15) NOT NULL,
  `NombrePlatilloR` VARCHAR(50) NOT NULL,
  `PrecioR` INT NOT NULL,
  `DescripcionR` VARCHAR(200) NOT NULL,
  `Cantidad` INT NOT NULL,
  `Mesa` VARCHAR(25) NOT NULL,
  `Fecha` VARCHAR(15) NOT NULL,
  PRIMARY KEY (`idPedidoR`),
  INDEX `fkPedidoRestauranteCliente_idx` (`idClienteR` ASC) VISIBLE,
  INDEX `fkPedidoRestaurantePlatillo_idx` (`idPlatilloR` ASC) VISIBLE,
  CONSTRAINT `fkPedidoRestauranteCliente`
    FOREIGN KEY (`idClienteR`)
    REFERENCES `dbproyectofinal`.`tclientes` (`idCliente`),
  CONSTRAINT `fkPedidoRestaurantePlatillo`
    FOREIGN KEY (`idPlatilloR`)
    REFERENCES `dbproyectofinal`.`tplatillos` (`idPlatillo`))
ENGINE = InnoDB
AUTO_INCREMENT = 7
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `dbproyectofinal`.`tpedidos`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `dbproyectofinal`.`tpedidos` (
  `idPedidos` INT NOT NULL AUTO_INCREMENT,
  `idPedidoRestaurante` INT NOT NULL,
  `idPedidoDocimilio` INT NOT NULL,
  PRIMARY KEY (`idPedidos`),
  INDEX `fkPedidosPedidoR_idx` (`idPedidoRestaurante` ASC) VISIBLE,
  INDEX `fkPedidosPedidoD_idx` (`idPedidoDocimilio` ASC) VISIBLE,
  CONSTRAINT `fkPedidosPedidoD`
    FOREIGN KEY (`idPedidoDocimilio`)
    REFERENCES `dbproyectofinal`.`tpedidodomicilio` (`idPedidoD`),
  CONSTRAINT `fkPedidosPedidoR`
    FOREIGN KEY (`idPedidoRestaurante`)
    REFERENCES `dbproyectofinal`.`tpedidorestaurante` (`idPedidoR`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `dbproyectofinal`.`tproveedores`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `dbproyectofinal`.`tproveedores` (
  `idProveedor` VARCHAR(15) NOT NULL,
  `EmpresaProveedor` VARCHAR(100) NOT NULL,
  `Nombre` VARCHAR(50) NOT NULL,
  `Contacto` VARCHAR(45) NOT NULL,
  `Correo` VARCHAR(50) NOT NULL,
  `DescripcionProducto` VARCHAR(200) NOT NULL,
  PRIMARY KEY (`idProveedor`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;



-- -----------------------------------------------------
-- Table `dbproyectofinal`.`tusuarios`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `dbproyectofinal`.`tusuarios` (
  `idUsuario` VARCHAR(15) NOT NULL,
  `Nombre` VARCHAR(50) NOT NULL,
  `Apellido` VARCHAR(50) NOT NULL,
  `Direccion` VARCHAR(80) NOT NULL,
  `Telefono` VARCHAR(25) NOT NULL,
  `Email` VARCHAR(45) NOT NULL,
  `TipoUsuario` VARCHAR(25) NOT NULL,
  `Estado` VARCHAR(25) NOT NULL,
  `Usuario` VARCHAR(45) NOT NULL,
  `Contraseña` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`idUsuario`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
