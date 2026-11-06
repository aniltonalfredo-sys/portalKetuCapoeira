# Portal — Instituto Ketu Capoeira

Monorepo com **portal institucional público** e **backoffice CMS** (NestJS + Prisma + MySQL + React/Vite).

Localização do projecto: `C:\Users\CPS\Desktop\portal-capoeira`

## Requisitos

- Node.js 20+
- Docker (MySQL na porta **3308**, para não conflituar com MySQL local em 3307) ou MySQL local com credenciais próprias

## Arranque rápido

```powershell
cd C:\Users\CPS\Desktop\portal-capoeira
docker compose up -d
copy backend\.env.example backend\.env
```

> **MySQL no Windows:** se tiver MySQL local (XAMPP, WAMP, serviço `mysqld`) na porta **3307**, o Docker usa **3308** para evitar conflito. A `DATABASE_URL` deve apontar para `127.0.0.1:3308`. Se a migration falhar com permissões, no contentor:  
> `docker exec portal-capoeira-mysql-1 mysql -uroot -proot -e "GRANT CREATE, ALTER, DROP, REFERENCES ON *.* TO 'portal'@'%'; FLUSH PRIVILEGES;"`

```powershell
npm install
npm run db:migrate
npm run db:seed
npm run dev
```

- Site público: http://localhost:5173  
- Backoffice: http://localhost:5173/admin  
- API: http://localhost:3000/api  

## Credenciais seed

| Perfil | Email | Password |
|--------|-------|----------|
| Administrador | `admin@escola.local` | `Admin123!` |
| Editor | `editor@escola.local` | `Editor123!` |

## Slugs institucionais (seed — Ketu)

| Página | URL pública |
|--------|-------------|
| A escola | `/p/sobre` |
| Mestre Cobra Coral | `/p/mestre-cobra-coral` |
| História do grupo | `/p/historia-do-grupo` |
| Graduação infantil | `/p/graduacao-infantil` |
| Graduação adulta | `/p/graduacao-adulta` |
| Graduação profissional | `/p/graduacao-profissional` |
| Formação e adaptação | `/p/formacao-e-adaptacao` |
| Uniforme e instrumentos | `/p/uniforme-e-instrumentos` |
| Toques de berimbau | `/p/toques-de-berimbau` |
| Cursos e aulões | `/p/cursos-e-auloes` |
| Valorização do Mestre | `/p/valorizacao-do-mestre` |
| Ética e disciplina | `/p/etica-e-disciplina` |
| Proposta objetiva | `/p/proposta-objetiva` |
| Terminologia Ketu | `/p/terminologia-ketu` |
| Troca de núcleos | `/p/troca-de-nucleos` |

Contactos oficiais: `mestrecobracoral@gmail.com`, `ketucapoeira@gmail.com`, [ketucapoeira.com.br](https://www.ketucapoeira.com.br)

## Deploy (resumo)

1. Definir `DATABASE_URL`, `JWT_SECRET` (mín. 32 caracteres), `CORS_ORIGIN`, `PUBLIC_BASE_URL`.
2. Correr migrations e seed (ou utilizador admin manual).
3. Servir `backend/uploads` com persistência (volume ou object storage).
4. Build frontend (`npm run build -w frontend`) e servir estáticos atrás de reverse proxy; proxy `/api` e `/uploads` para o NestJS.
5. Backup regular da base de dados e da pasta de media.

## Estrutura

- `backend/` — API NestJS, Prisma, uploads
- `frontend/` — React (`src/public`, `src/admin`, `src/shared`)
- `docs/BACKLOG-FASE-C.md` — funcionalidades pós-MVP
