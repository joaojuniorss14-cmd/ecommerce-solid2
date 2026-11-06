# E-commerce SOLID - Projeto 2

Projeto 1 refatorado, agora usando InversifyJS para injetar as dependencias.
O arquivo `src/container/container.ts` e onde tudo e montado e onde o `APP_ENV` escolhe o modo.

## Como rodar

Precisa do Node.js instalado.

```bash
npm install
cp .env.example .env
npm run prisma:migrate
npm run prisma:seed
npm run dev
```

No Windows, no lugar do `cp` use: `copy .env.example .env`

A API sobe em `http://localhost:3000`.

## Modos

O modo e escolhido no arquivo `.env`, mudando so a linha `APP_ENV`. Depois e so reiniciar.

| | APP_ENV=dev | APP_ENV=test |
|---|---|---|
| E-mail | EtherealMailProvider (precisa de internet) | ConsoleMailProvider (mostra no console) |
| Pedidos | PrismaOrderRepository (salva no SQLite) | InMemoryOrderRepository (fica num array) |

Se nao tiver `APP_ENV`, usa `dev`. O modo `test` funciona sem internet.
Os produtos vem do SQLite nos dois modos, entao tem que rodar o migrate e o seed antes.

## Testando

```bash
curl -X POST http://localhost:3000/orders \
-H "Content-Type: application/json" \
-d '{
  "customer": "cliente@ethereal.email",
  "items": [{ "productId": 1, "quantity": 1 }],
  "paymentMethod": "credit_card",
  "paymentDetails": { "cardNumber": "1234567812345678", "cvv": "123" }
}'
```

Produto 1 (livro fisico) da R$ 110 e produto 2 (e-book) da R$ 50, nos dois modos.
Formas de pagamento: `credit_card`, `debit_card` e `pix`.
