---
publish: false
---

### Módulo de validação de CPF(validation-br)
Biblioteca de validação de documentos pessoais no Brasil, como: CPF, CNPJ, CNH, Telefone, Placa de carro, Chave Pix, Renavam, Processo Judiciais, etc.

O validation-br permite a criação de números fakes para facilitar o desenvolvimento de testes, além de aplicar máscaras e calcular somente os dígitos verificadores.

#### Instalação
```
# Usando pnpm
pnpm add validation-br
# Usando npm
npm install validation-br
```
#### Exemplo de Uso
```
import {isCpf} from 'validation-br';
const myCpf = "259.324.940-42"

const cpfValid = isCpf(myCpf);
if(cpfValid){
	return cpfValid
}else{
	throw new BadRequestException("Cpf invalid");
}
```

