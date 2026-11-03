# Changelog — schematize-analytics

Todas as mudanças relevantes deste pacote, no formato [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/),
com versionamento [SemVer](https://semver.org/lang/pt-BR/).

## [Não lançado]
### Corrigido
- `check-tracking.sh`: o init do SDK só passa SOB condição de consentimento (if/&&/listener nas 8 linhas anteriores, comentários ignorados) ou em modo sem cookie/sem persistência na configuração; palavra "consent" solta no arquivo ou em comentário e `opt_out` não valem mais (opt-in, piso 4). 4 testes novos (3 vermelhos antes).
### Adicionado
- Regra "analytics é best-effort e independente do coletor" (pisos 10/28); bloco "Herda os pisos 22–29".
### Pendente (on-hold)
- `[~]` nome de evento dinâmico/coleta por HTTP direto no gate e verificação de chave de prd em `.env` não-prd (P2): sem decisão de heurística.

## [0.2.0] — 2026-10-14
Integração ao catálogo: orçamento de description e ponteiros entre as irmãs novas.

### Corrigido

- `check-tracking.sh` sai com o status real (sem `exit 0` incondicional no fim).

### Alterado
- `description` <=190 (orçamento do catálogo).
- Divisas: `schematize-incident → references/lgpd.md` (vazamento de dado de tracking) e `schematize-payments` (dado financeiro não é tracking).
- Motivo: o catálogo estourou o orçamento de listagem com 45 skills; cada fronteira aponta a dona em vez de duplicar.

## [0.1.0] — 2026-10-14
Primeira versão. Medição de comportamento de produto vivia espalhada: privacidade/LGPD na base e na
`schematize-data`, telemetria técnica na `schematize-observability`, tráfego orgânico na `schematize-seo`.
Faltava a dona de quem decide **o que medir, com que direito e com que método** — e o resultado era evento
sem dono, e-mail dentro de propriedade, "ativação" com três definições e teste A/B encerrado no primeiro
p < 0,05.

### Adicionado
- `SKILL.md` com 14 pisos: tracking plan como contrato, nome `objeto_acao`, sem PII, consentimento, first-party,
  métrica de definição única, retenção por coorte, desenho de experimento antes de rodar, flags com dono, ambientes
  separados, telemetria técnica fora, ADR.
- `references/`: `plano-de-tracking`, `consentimento-lgpd`, `ferramentas` (PostHog, Plausible, Umami, GA4),
  `metricas`, `experimentacao` (amostra, SRM, peeking, guardrails), `feature-flags`, `stack-versoes` (anexo volátil).
- Gate `scripts/check-tracking.sh` (evento não declarado, propriedade fora do plano, nome fora do padrão, evento sem
  dono/duplicado, PII por chave/valor/campo do usuário, `identify` com PII, SDK sem consentimento) e
  `check-tracking.test.sh` com casos vermelhos e verdes plantados; PII de teste montada em tempo de execução.
- Comandos `/analytics-help`, `-load`, `-claude`, `-handoff`, `-cc`, `-plan`, `-review`, `-consent`, `-metric`,
  `-experiment`; `assets/CLAUDE.md` e `assets/tracking-plan.example.yml`.
