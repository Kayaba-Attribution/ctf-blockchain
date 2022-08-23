# Desafíos tipo CTF en Blockchain

Este repositorio recopila desafíos de blockchain en CTF y juegos de guerra.

Estos desafíos están categorizados por tema, pero no están ordenados por dificultad o por recomendación.

Algunos desafíos se derivan de mis hazañas (por ejemplo, [Ethernaut](src/Ethernaut/), [Paradigm CTF 2021](src/ParadigmCTF2021/)).

Si hay descripciones incorrectas, les agradecería que me lo hiciera saber a través de un issue o PR

| English | [日本語](README_JA.md) | [Español](README_ES.md) |
| ------- | ---------------------- | ---------------------- |

---

**Tabla de contenido**
- [Ethereum](#etereum)
  - [Ethereum/Conceptos básicos](#ethereumcontract-basics)
  - [rompecabezas EVM](#evm-puzzles)
  - [Uso indebido de `tx.origin`](#misuse-of-txorigin)
  - [Los números pseudoaleatorios generados on-chain son predecibles](#pseudorandom-numbers-generated-on-chain-are-predictable)
  - [Conceptos básicos de ERC-20](#erc-20-basic)
  - [Almacenamiento sobrescrito por `delegatecall`](#storage-overwrite-by-delegatecall)
  - [Discordancia de contexto en `delegatecall`](#context-mismatch-in-delegatecall)
  - [Desbordamiento de enteros](#integer-overflow)
  - [Las transferencias de Ether a un contrato no siempre son ejecutables](#ether-transfers-to-a-contract-are-not-always-executable)
  - [Transferencia forzada de Ether a un contrato mediante `selfdestruct`](#forced-ether-transfer-to-a-contract-via-selfdestruct)
  - [No todos los procesos pueden ejecutarse después de una llamada de contrato](#not-all-procedures-can-be-executed-after-a-contract-call)
  - [Olvidarse de establecer `view`/`pure` en funciones de interfaz y contrato abstracto](#forgetting-to-set-viewpure-to-interface-and-abstract-contract-functions)
  - [Las funciones `view` no siempre devuelven el mismo valor](#view-functions-do-not-always-return-the-same-value)
  - [Errores al configurar `almacenamiento` y `memoria`](#mistakes-in-setting-storage-and-memory)
  - [Seguimiento de transacciones](#transaction-tracing)
  - [Revertir estados (los contratos no deben contener datos confidenciales)](#reversing-states-contracts-must-not-contain-confidential-data)
  - [Revertir transacciones](#reversing-transactions)
  - [Revertir el bytecode de la EVM](#reversing-evm-bytecode)
  - [EVM bytecode golf](#evm-bytecode-golf)
  - [Optimización de gas](#gas-optimization)
  - [Ataque de reingreso](#re-entrancy-attack)
  - [Conceptos básicos de préstamo flash](#flash-loan-basics)
  - [Derechos masivos mediante la ejecución de préstamos flash durante snapshots](#massive-rights-by-executing-flash-loans-during-snapshots)
  - [Evitar reembolsos de préstamos flash con arquitectura push](#bypassing-repayments-of-push-architecture-flash-loans)
  - [Error en el algoritmo de cálculo de precios de AMM](#bug-in-amm-price-calculation-algorithm)
  - [Ataque usando tokens personalizados](#attack-using-custom-tokens)
  - [Fuga de fondos debido a la manipulación de Oracle (sin préstamos flash)](#funds-leakage-due-to-oracle-manipulation-without-flash-loans) 
  - [Fuga de fondos debido a la manipulación del oráculo (con préstamos flash)](#funds-leakage-due-to-oracle-manipulation-with-flash-loans)
  - [Ataque sándwich](#sandwich-attack)
  - [Recuperación de una clave privada usando ataque de mismo nonce](#recovery-of-a-private-key-by-same-nonce-attack)
  - [Clacular address usando fuerza bruta](#brute-force-address)
  - [Recuperación de una clave pública](#recovery-of-a-public-key)
  - [Cifrado y descifrado en secp256k1](#encryption-and-decryption-in-secp256k1)
  - [Omitir bot y tomar un token ERC-20 propiedad de una billetera con una clave privada conocida](#bypassing-bot-and-taking-an-erc-20-token-owned-by-a-wallet-with-a-known-private-key)
  - [Sobrescritura de almacenamiento arbitrario estableciendo una longitud de un array a `2^256-1` (< Solidity 0.6.0)](#arbitrary-storage-overwriting-by-setting-an-array-length-to-2256-1--solidity-060)
  - [Constructor es solo una función con un error tipográfico (< Solidity 0.5.0)](#constructor-is-just-a-function-with-a-typo--solidity-050)
  - [Sobrescritura de almacenamiento mediante puntero de almacenamiento no inicializado (< Solidity 0.5.0)](#storage-overwrite-via-uninitialized-storage-pointer--solidity-050)
  - [Otras vulnerabilidades y métodos ad-hoc](#other-ad-hoc-vulnerabilities-and-methods)
- [Bitcoin](#bitcoin)
  - [Conceptos básicos de Bitcoin](#bitcoin-basics)
  - [Recuperación de una clave privada usando ataque de mismo nonce](#recovery-of-a-private-key-by-same-nonce-attack-1)
  - [Evitar PoW de otras aplicaciones usando la base de datos PoW de Bitcoin](#bypassing-pow-of-other-applications-using-bitcoins-pow-database)
- [Solana](#solana)
- [Otros relacionados con blockchain](#other-blockchain-related)
  - [IPFS](#ipfs)

---