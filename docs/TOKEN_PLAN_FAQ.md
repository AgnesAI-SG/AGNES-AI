# Token Plan FAQ

Last updated: `2026-06-28 00:00 Asia/Singapore`

This page summarizes current public reference values for Agnes AI access types, API key behavior, RPM limits, and Token Plan subscription quotas.

The base Token Plan quota reference was published on `2026-06-22`. Video model RPM values were updated on `2026-06-28`.

> These values are operational reference values. Agnes AI may adjust rate limits, quota rules, model availability, or pricing based on infrastructure capacity, service stability, abuse prevention, product policy, or model availability.

## Access Types

Agnes AI currently supports three access types.

| Access type | Description |
| --- | --- |
| Free / default user | User without Token Plan subscription or enterprise verification. |
| Enterprise-verified user | User with enterprise verification and higher baseline limits. |
| Token Plan user | User with Token Plan subscription, higher RPM, and subscription quotas. |

A user may hold multiple access types at the same time, such as a free key, an enterprise key, and a Token Plan key. Each key type uses its own limit pool.

## Token Plan Subscription Quotas

RPM limits and subscription quotas apply at the same time.

| Plan | `agnes-2.0-flash` | `agnes-image-2.0 / 2.1-flash` | `agnes-video-v2.0` |
| --- | --- | --- | --- |
| Starter | 1,500 requests per 5 hours; 15,000 requests per week | 4,000 images per day | 500 seconds per day |
| Plus | 7,500 requests per 5 hours; 75,000 requests per week | 4,000 images per day | 500 seconds per day |
| Pro | 30,000 requests per 5 hours; 300,000 requests per week | 4,000 images per day | 500 seconds per day |

Quota accounting:

- Text quotas are counted by request.
- Image quotas are counted by generated image.
- Video quotas are counted by generated video duration in seconds.
- Token Plan users are subject to both RPM limits and subscription quotas.

## Text Model RPM

| Model type | User type | Public request RPM | Actual executable RPM |
| --- | --- | ---: | ---: |
| Text models | Free / default | 30 | 20 |
| Text models | Enterprise | 60 | 40 |
| Text models | Token Plan | 1,000 | 1,000 |

## Image Model RPM

Image model RPM is resolution-specific. Higher resolutions usually have lower RPM because they consume more compute.

| Model type | User type | Resolution | Public request RPM | Actual executable RPM |
| --- | --- | --- | ---: | ---: |
| Image models | Free / default | 1K | 30 | 20 |
| Image models | Free / default | 2K | 20 | 10 |
| Image models | Free / default | 3K | 2 | 1 |
| Image models | Free / default | 4K | 1 | 1 |
| Image models | Enterprise | 1K | 60 | 40 |
| Image models | Enterprise | 2K | 40 | 20 |
| Image models | Enterprise | 3K | 2 | 1 |
| Image models | Enterprise | 4K | 2 | 1 |
| Image models | Token Plan | 1K | 120 | 100 |
| Image models | Token Plan | 2K | 120 | 80 |
| Image models | Token Plan | 3K | 2 | 1 |
| Image models | Token Plan | 4K | 2 | 1 |

## Video Model RPM

Video generation is subject to both RPM limits and daily generated-video duration quotas.

| Model type | User type | Public request RPM | Actual executable RPM |
| --- | --- | ---: | ---: |
| Video models | Free / default | 2 | 1 |
| Video models | Enterprise | 2 | 2 |
| Video models | Token Plan | 6 | 5 |

Token Plan video quota remains `500 seconds per day`.

## RPM vs. Subscription Quotas

RPM controls request frequency. For example:

- Free / default video model access: `1` actual RPM.
- Enterprise video model access: `2` actual RPM.
- Token Plan video model access: `5` actual RPM.

Subscription quota controls total usage within a time window. For example:

- Starter users can send 1,500 `agnes-2.0-flash` requests per 5 hours.
- Token Plan users can generate 4,000 images per day.
- Token Plan users can generate 500 seconds of video per day.

Both limits apply at the same time. For example, Token Plan Pro users may have `1,000` actual text-model RPM, but still remain subject to the Pro quota of 30,000 requests per 5 hours and 300,000 requests per week.

## API Key Types and Limit Pools

| API key type | Applies to | Limit behavior |
| --- | --- | --- |
| Free / default key | All users | Uses the free / default RPM pool. |
| Enterprise key | Enterprise-verified users | Uses the enterprise RPM pool. |
| Token Plan key | Token Plan users | Uses the Token Plan RPM and subscription quota pool. |

Limits are shared by key type, not by each individual key. Creating multiple keys of the same type does not increase total RPM or quota.

| Scenario | Limit behavior |
| --- | --- |
| Two free keys | Share the same free / default RPM pool. |
| Two enterprise keys | Share the same enterprise RPM pool. |
| Two Token Plan keys | Share the same Token Plan RPM and subscription quota pool. |

Different key types use separate pools. For example, a free key and a Token Plan key do not share the same limit pool.

## Recommended Use Cases

| User type | Recommended use cases |
| --- | --- |
| Free / default | Basic testing, lightweight personal use, low-frequency integration. |
| Enterprise | Business users, team testing, higher baseline throughput. |
| Token Plan | Production use, high-frequency requests, agent workflows, multi-user applications, frequent image or video generation. |

## FAQ

### Do multiple API keys increase RPM or quota?

No. Multiple keys of the same type share the same limit pool.

### Can Token Plan users still use free keys?

Yes. Free keys and Token Plan keys use different limit pools.

### Can Token Plan users also become enterprise-verified users?

Yes. After enterprise verification, a user may use free / default keys, enterprise keys, and Token Plan keys. Each key type follows its own limit pool.

### Does enterprise verification automatically grant Token Plan quota?

No. Enterprise verification provides higher baseline RPM. Token Plan quota applies only after subscribing to Token Plan.

### Are image quotas counted by request or by generated image?

Image quotas are counted by generated image. Current Token Plan reference quota for `agnes-image-2.0 / 2.1-flash` is 4,000 images per day.

### Are video quotas counted by request or by video duration?

Video quotas are counted by generated video duration. Current Token Plan reference quota for `agnes-video-v2.0` is 500 seconds per day. Video RPM limits also apply.
