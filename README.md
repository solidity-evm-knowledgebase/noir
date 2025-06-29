# Noir

## Architecture

### Nargo

- CLI tool.
- Enables us to compile our circuits and execute them.
- noirup to install latest version of nargo
- nargo will compile our circuits to create ACIR, the intermediate representation used by the backend.
- Execute creates the witness (it will also compile the circuits)

### Barretenberg (backend)

- Using the backend, we can generate proofs and verify those proofs, by using the witness and ACIR files we generated.
- Verification can be done either offchain or onchain (via Verify smart contract).
