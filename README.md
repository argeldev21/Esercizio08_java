Codice SQL per la creazione delle tabelle, chiavi e vincoli di integrità:

-- TABELLA CLIENTI
CREATE TABLE clienti (
    id_cliente INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    indirizzo_spedizione VARCHAR(255) NOT NULL
);

-- TABELLA PRODOTTI
CREATE TABLE prodotti (
    id_prodotto INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    descrizione TEXT,
    prezzo DECIMAL(10,2) NOT NULL CHECK (prezzo >= 0),
    quantita_magazzino INT NOT NULL CHECK (quantita_magazzino >= 0)
);

-- TABELLA ORDINI
CREATE TABLE ordini (
    id_ordine INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT NOT NULL,
    data_ordine DATE NOT NULL,
    stato ENUM('In elaborazione', 'Spedito', 'Consegnato', 'Annullato') NOT NULL,
    FOREIGN KEY (cliente_id) REFERENCES clienti(id_cliente)
);

-- TABELLA DETTAGLIO ORDINI
CREATE TABLE dettaglio_ordini (
    id_dettaglio INT PRIMARY KEY AUTO_INCREMENT,
    ordine_id INT NOT NULL,
    prodotto_id INT NOT NULL,
    quantita INT NOT NULL CHECK (quantita > 0),
    prezzo_unitario DECIMAL(10,2) NOT NULL CHECK (prezzo_unitario >= 0),
    FOREIGN KEY (ordine_id) REFERENCES ordini(id_ordine),
    FOREIGN KEY (prodotto_id) REFERENCES prodotti(id_prodotto)
);
