# @aero/web-moniter

Web监控SDK入口包 - 整合所有功能

## 安装

```bash
npm install @aero/web-moniter
# 或
yarn add @aero/web-moniter
# 或
pnpm add @aero/web-moniter
```

## 基本使用

```javascript
import moniter from '@aero/web-moniter';
// 引入需要的插件
import jsErrorPlugin from '@aero/plugins/js-error'
import networkPlugin from '@aero/plugins/network'
import performancePlugin from '@aero/plugins/performance'

// 初始化监控
moniter.init({
  // 必填项
  project: 'my-app',
  
  // 可选配置
  version: '1.0.0',
  environment: 'production',
  userId: 'user-123',
  
  // 上报配置
  reportUrl: 'https://your-api-endpoint.com/collect'
});

// 使用插件
moniter.use([
  [jsErrorPlugin],
  [networkPlugin, { ignoreUrls: ['/health'] }],
  [performancePlugin]
]);

// 手动上报错误
moniter.addError(new Error('自定义错误'), { 
  category: 'business', 
  level: 'error' 
});

// 手动上报指标数据
moniter.send({
  name: 'custom_metric',
  value: 100,
  tags: { module: 'payment' }
});

// 销毁实例
// moniter.destroy();
```

## 特性

- **一站式监控解决方案**：一个包即可获得完整的前端监控能力
- **简单配置**：提供简化的配置项，易于使用
- **全面覆盖**：包含错误监控、性能监控、网络请求监控等多种监控类型
- **可扩展**：支持通过插件系统扩展功能

## 包含模块

该包整合了以下子包的功能：
- `@aero/core` - 核心监控能力
- `@aero/plugins` - 内置插件集合
- `@aero/reporter` - 数据上报功能
- `@aero/types` - TypeScript 类型定义

## 许可证

ISC