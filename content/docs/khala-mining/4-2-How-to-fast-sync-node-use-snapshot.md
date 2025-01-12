---
title: "3.2 How to accelerate your node syncing if you haven't fully synced yet"
---

## Problem

If your node is not up-to-date, a typical node log looks like

```
2021-09-15 13:33:27 [Relaychain] ⚙️  Syncing 10.4 bps, target=#9236775 (20 peers), best: #9227955 (0xa897…4f36), finalized #9227895 (0x1d6d…1527), ⬇ 1.7MiB/s ⬆ 657.8kiB/s
2021-09-15 13:33:27 [Parachain] ⚙️  Syncing 40.4 bps, target=#400531 (1 peers), best: #396657 (0xb898…6c02), finalized #396443 (0xf470…2f54), ⬇ 378.7kiB/s ⬆ 1.6kiB/s
```

and `best` is too far from `target`.

This article shares a cheat way to accelerate your node syncing.

ATTENTION: If your node is near the newest block height (about several hours to catch up) or has already caught up,
you don't need to do anything, just sit and wait.

## Download latest snapshot (Updated in 9/18/2021)

We recommend to use the BT download with <a href="/files/khala-snapshot-2021-09-17.torrent">torrent</a>. You can check the SHA256 checksum of the torrent

```
$ sha256sum khala-snapshot-2021-09-17.torrent
595e448bfce90c6725de75d1f38462570d7142c41199375bc86d35f6809b733f  khala-snapshot-2021-09-17.torrent
```

Extract when downloaded, you shall get `khala-node` folder.

ATTENTION: snapshot archive is ~220GB, extract requires ~350GB, which means you require at least 600GB free disk space, if you don't have enough space, consider extract to external storage.

**Updated in 9/18/2021**: We have updated the snapshot which does not contain broken data anymore.

> There are community maintained snapshots updated more frequently. (Thanks to zozyo on our forum.) You may consider using at your own risk:
>
> - <https://forum.phala.network/t/topic/2852>

## Preparation

Please ensure Phala services are stopped, especially the node, if you're using solo mining, use

```bash
sudo phala stop
```

to stop Phala services.

## Replace local data with extracted snapshot

### If you're a solo miner

Delete all files and folders inside `/var/khala-dev-node`，move all files and folders from `khala-node` into `/var/khala-dev-node`

If you do things right, inside `/var/khala-dev-node` it looks like

```
$ ls /var/khala-dev-node
chains  polkadot
```

### Advanced miner

Find the node working directory, Delete all files and folders inside the directory, then move all files and folders from `khala-node` into it.

## Restart Phala services

If you're a solo miner, do

```bash
sudo phala start
```

to restart services, then you shall find out your node has fast forward to a very close to latest status, then waiting few minutes or hours,  then the node will catch up, and you can start mining now.
