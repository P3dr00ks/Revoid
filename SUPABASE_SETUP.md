# Configurar sincronização Supabase

O site permanece estático no GitHub Pages. Cada pessoa precisa usar um projeto Supabase próprio e entrar com sua própria conta. A chave publicável/anon pode ficar no navegador; **nunca use nem publique a chave `service_role`**.

## 1. Criar tabela e políticas

No projeto Supabase, abra **SQL Editor**, crie uma consulta e execute:

```sql
create table if not exists public.entries (
  id text not null,
  user_id uuid not null references auth.users(id) on delete cascade,
  record_date date not null,
  record_time text,
  activity_type text not null check (activity_type in ('Venda', 'Assistência', 'Outro')),
  sale_number text,
  title text not null,
  seller text,
  service_status text,
  details text,
  updated_at timestamptz not null default now(),
  primary key (user_id, id)
);

alter table public.entries enable row level security;
revoke all on public.entries from anon;
grant select, insert, update, delete on public.entries to authenticated;

drop policy if exists "Users manage their own entries" on public.entries;
create policy "Users manage their own entries"
on public.entries for all to authenticated
using (auth.uid() = user_id)
with check (auth.uid() = user_id);
```

## 2. Ajustar autenticação

Em **Authentication → URL Configuration**, configure o Site URL e adicione a URL do GitHub Pages à lista de Redirect URLs, por exemplo `https://p3dr00ks.github.io/Revoid/`.

## 3. Conectar o site

Em **Project Settings → API**, copie a Project URL e a chave **Publishable** (ou `anon` legacy). No painel “Sincronização online · Supabase” do REVOID, salve esses valores e entre ou crie uma conta. A senha é enviada diretamente ao Supabase Auth e não é armazenada pelo REVOID.

O primeiro uso em um aparelho novo apenas baixa e combina os registros. Para enviar os registros locais existentes à nuvem, use “Sincronizar meus registros” e confirme a quantidade apresentada. Depois, novos registros, edições e exclusões são sincronizados automaticamente quando a sessão estiver ativa. Faça exportação JSON de backup regularmente.


