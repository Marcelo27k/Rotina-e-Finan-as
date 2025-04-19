# Rotina-e-Finan-as
// Importações básicas
import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Card, CardContent } from "@/components/ui/card";
import { motion } from "framer-motion";

// Landing Page
export default function App() {
  const [loggedIn, setLoggedIn] = useState(false);
  const [showSignIn, setShowSignIn] = useState(false);

  return (
    <div className="min-h-screen bg-[#474647] text-white">
      {!loggedIn ? (
        <div className="flex flex-col items-center justify-center min-h-screen px-4 text-center">
          <h1 className="text-4xl font-bold mb-4 text-[#2D7DD2]">Bem-vindo ao Lovable</h1>
          <p className="text-[#FABC3C] mb-6">Organize sua rotina, finanças e dívidas em um só lugar</p>
          <Button 
            className="bg-[#E3170A] hover:bg-[#B30E08] text-white px-6 py-3 rounded-2xl text-lg"
            onClick={() => setShowSignIn(true)}
          >
            Login / Sign In
          </Button>
        </div>
      ) : (
        <Dashboard />
      )}

      {showSignIn && (
        <div className="fixed inset-0 bg-black/50 flex items-center justify-center px-4">
          <Card className="w-full max-w-md bg-[#7CDEDC] text-black">
            <CardContent className="p-6 space-y-4">
              <h2 className="text-xl font-bold text-center">Acesse sua conta</h2>
              <Input placeholder="E-mail" type="email" className="bg-white" />
              <Input placeholder="Senha" type="password" className="bg-white" />
              <Button 
                className="bg-[#2D7DD2] hover:bg-[#226AB6] w-full"
                onClick={() => {
                  setLoggedIn(true);
                  setShowSignIn(false);
                }}
              >
                Entrar
              </Button>
            </CardContent>
          </Card>
        </div>
      )}
    </div>
  );
}

// Página após login com notas, finanças e dívidas
function Dashboard() {
  const notas = [
    { id: 1, titulo: "Pagar fatura Nubank", descricao: "Dia 25/04 - R$ 500" },
    { id: 2, titulo: "Reunião com fornecedor", descricao: "Segunda-feira às 10h" },
    { id: 3, titulo: "Atualizar gastos Inter", descricao: "Revisar entradas da semana" },
  ];

  const financas = [
    { banco: "Nubank", tipo: "Entrada", valor: 1200 },
    { banco: "Inter", tipo: "Saída", valor: 450 },
    { banco: "Itaú", tipo: "Entrada", valor: 890 },
    { banco: "Neon", tipo: "Saída", valor: 300 },
  ];

  const dividas = [
    { nome: "Cartão Nubank", valor: 1500, parcelas: 3, vencimento: "25/04" },
    { nome: "Empréstimo Itaú", valor: 2200, parcelas: 6, vencimento: "10/05" },
  ];

  return (
    <div className="p-4 space-y-8">
      <section>
        <header className="flex justify-between items-center mb-4">
          <h2 className="text-2xl font-semibold text-[#FABC3C]">Minhas Notas</h2>
          <Button className="bg-[#7CDEDC] text-black px-4 py-2 text-sm rounded-md md:text-base md:px-6 md:py-3">
            Nova Nota
          </Button>
        </header>

        <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
          {notas.map((nota) => (
            <Card key={nota.id} className="bg-[#2D7DD2] text-white">
              <CardContent className="p-4">
                <h3 className="font-bold text-lg">{nota.titulo}</h3>
                <p>{nota.descricao}</p>
              </CardContent>
            </Card>
          ))}
        </div>
      </section>

      <section>
        <h2 className="text-xl font-semibold text-[#2D7DD2] mb-2">Finanças por Banco</h2>
        <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-4">
          {financas.map((item, index) => (
            <Card key={index} className="bg-[#7CDEDC] text-black">
              <CardContent className="p-4">
                <p className="font-bold">{item.banco}</p>
                <p>{item.tipo}: R$ {item.valor}</p>
              </CardContent>
            </Card>
          ))}
        </div>
      </section>

      <section>
        <h2 className="text-xl font-semibold text-[#E3170A] mb-2">Painel de Dívidas</h2>
        <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
          {dividas.map((d, i) => (
            <Card key={i} className="bg-[#FABC3C] text-black">
              <CardContent className="p-4">
                <p className="font-bold">{d.nome}</p>
                <p>Total: R$ {d.valor}</p>
                <p>Parcelas: {d.parcelas}</p>
                <p>Vencimento: {d.vencimento}</p>
              </CardContent>
            </Card>
          ))}
        </div>
      </section>
    </div>
  );
}
