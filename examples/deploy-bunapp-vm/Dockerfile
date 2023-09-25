FROM oven/bun AS builder

WORKDIR /dist

COPY package.json package.json
COPY bun.lockb bun.lockb

RUN bun install

COPY . .

RUN bun build ./main.ts --compile --outfile main

FROM oven/bun AS release

WORKDIR /

COPY --from=builder /dist/main /main

EXPOSE 5000

CMD ["bun","run","main"]


