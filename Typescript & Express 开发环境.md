# typescript & express 开发环境

## 功能

1. typescript 语法。
2. 监听文件自动编译。

## 依赖

1. express  (Fast, unopinionated, minimalist web framework for node.)
2. typescript (TypeScript is a superset of JavaScript that compiles to clean JavaScript output.)
3. ts-node (TypeScript execution and REPL for node.js)
4. tsconfig-paths (Load node modules according to tsconfig paths, in run-time or via API)
5. nodemon (Monitor for any changes in your node.js application and automatically restart the server - perfect for development)

## 目录结构

```
.
├── src
├── build
├── package.json
├── nodemon.json
└── tsconfig.json
```

package.json

```json
{
    "dependencies": {
        "@types/express": "^4.17.7",
        "express": "^4.17.1",
        "nodemon": "^2.0.4",
        "ts-node": "^8.10.2",
        "tsconfig-paths": "^3.9.0",
        "typescript": "^3.9.7"
    },
}

```

nodemon.json

```json
{
    "verbose": false,
    "debug": false,
    "exec": "ts-node -r tsconfig-paths/register ./src/index.ts",
    "ignore": [
        "mochawesome-report",
        "node_modules",
        "./test",
        "**/*.d.ts",
        "*.test.ts",
        "*.spec.ts",
        "fixtures/*",
        "test/**/*",
        "docs/*"
    ],
    "events": {
        "restart": ""
    },
    "watch": ["./src/index.ts", "./configs"],
    "ext": "ts tsx",
    "inspect": true
}
```

tsconfig.json

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "outDir": "./build",
    "rootDir": "./src",
    "baseUrl": "./",
    "paths": {
      "@/*": ["./src/*"]
    },
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```