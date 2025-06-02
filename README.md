import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

export default function MuseedApp() {
  const [user, setUser] = useState(null);
  const [isRegistering, setIsRegistering] = useState(false);
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [artTitle, setArtTitle] = useState("");
  const [artUrl, setArtUrl] = useState("");
  const [posts, setPosts] = useState([
    { id: 1, title: "Luz e sombra", image: "https://source.unsplash.com/random/300x300?sig=1" },
    { id: 2, title: "Expressão em azul", image: "https://source.unsplash.com/random/300x300?sig=2" },
  ]);

  const handleLogin = (e) => {
    e.preventDefault();
    setUser({ email });
  };

  const handleRegister = (e) => {
    e.preventDefault();
    setUser({ email });
  };

  const handleCreatePost = (e) => {
    e.preventDefault();
    const newPost = {
      id: posts.length + 1,
      title: artTitle,
      image: artUrl,
    };
    setPosts([newPost, ...posts]);
    setArtTitle("");
    setArtUrl("");
  };

  if (!user) {
    return (
      <div className="min-h-screen bg-neutral-100 text-neutral-900 p-4">
        <header className="text-center py-6">
          <h1 className="text-4xl font-bold tracking-wide">Museed</h1>
          <p className="text-lg mt-2 max-w-xl mx-auto text-neutral-600">
            Um espaço sensível e vibrante para artistas expressarem suas múltiplas formas de arte. Compartilhe, descubra e inspire-se.
          </p>
        </header>

        <main className="max-w-md mx-auto bg-white p-6 rounded-2xl shadow-md">
          <h2 className="text-2xl font-semibold mb-4">
            {isRegistering ? "Cadastro" : "Entrar"}
          </h2>
          <form onSubmit={isRegistering ? handleRegister : handleLogin} className="flex flex-col gap-4">
            <Input
              type="email"
              placeholder="Seu e-mail"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
            />
            <Input
              type="password"
              placeholder="Sua senha"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
            />
            <Button type="submit" className="w-full">
              {isRegistering ? "Cadastrar" : "Entrar"}
            </Button>
          </form>
          <p className="text-sm text-neutral-500 mt-4 text-center">
            {isRegistering ? "Já tem uma conta?" : "Não tem uma conta?"}{" "}
            <button
              onClick={() => setIsRegistering(!isRegistering)}
              className="text-blue-500 hover:underline"
            >
              {isRegistering ? "Entrar" : "Cadastre-se"}
            </button>
          </p>
        </main>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-neutral-100 text-neutral-900 p-4 flex flex-col">
      <header className="text-center py-6">
        <h1 className="text-4xl font-bold tracking-wide">Museed</h1>
        <p className="text-lg mt-2 max-w-xl mx-auto text-neutral-600">
          Bem-vindo(a), {user.email}! Compartilhe sua arte com o mundo.
        </p>
      </header>

      <main className="max-w-4xl mx-auto grid gap-8 flex-grow">
        <section className="bg-white p-6 rounded-2xl shadow-md">
          <h2 className="text-2xl font-semibold mb-4">Nova arte</h2>
          <form onSubmit={handleCreatePost} className="flex flex-col gap-4">
            <Input
              placeholder="Título da arte"
              value={artTitle}
              onChange={(e) => setArtTitle(e.target.value)}
            />
            <Input
              placeholder="URL da imagem da arte"
              value={artUrl}
              onChange={(e) => setArtUrl(e.target.value)}
            />
            <Button type="submit">Publicar</Button>
          </form>
        </section>

        <section>
          <h2 className="text-2xl font-semibold mb-4">Galeria</h2>
          <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
            {posts.map((post) => (
              <Card key={post.id} className="overflow-hidden">
                <img src={post.image} alt={post.title} className="w-full h-48 object-cover" />
                <CardContent className="p-4">
                  <p className="text-sm text-neutral-700 font-medium">{post.title}</p>
                </CardContent>
              </Card>
            ))}
          </div>
        </section>
      </main>

      <footer className="text-center text-sm text-neutral-500 py-4 mt-8 border-t border-neutral-300">
        © 2025 Museed • por Samara<br />
        Pensado por Samara com a ajuda de Endi Ranielly, Ana Cecília, Lucas Alves, Isabella e Nicolle.
      </footer>
    </div>
  );
}
