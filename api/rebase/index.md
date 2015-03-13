---
layout: default
menu_item: api
title: Rebase
description: Version 0.3.0
menu_item: api
return_to:
  "API Documentation Index": /api/
sections:
  "init": "#init"
  "initOptions": "#initOptions"
  "open": "#open"
  "#abort": "#abort"
  "#commit": "#commit"
  "#finish": "#finish"
  "#free": "#free"
  "#operationByIndex": "#operationByIndex"
  "#operationCurrent": "#operationCurrent"
  "#operationEntrycount": "#operationEntrycount"
---

## <a name="init"></a><span>Rebase.</span>init <span class="tags"><span class="async">Async</span><span class="experimental">Experimental</span></span>

```js
Rebase.init(repo, branch, upstream, onto, signature, opts).then(function(rebase) {
  // Use rebase
});
```

| Parameters | Type |   |
| --- | --- | --- |
| repo | [Repository](/api/repository/) | The repository to perform the rebase |
| branch | [AnnotatedCommit](/api/annotated_commit/) | The terminal commit to rebase |
| upstream | [AnnotatedCommit](/api/annotated_commit/) | The commit to begin rebasing from, or NULL to rebase all reachable commits |
| onto | [AnnotatedCommit](/api/annotated_commit/) | The branch to rebase onto, or NULL to rebase onto the given upstream |
| signature | [Signature](/api/signature/) | The signature of the rebaser (optional) |
| opts | [RebaseOptions](/api/rebase_options/) | Options to specify how rebase is performed |

| Returns |  |
| --- | --- |
| [Rebase](/api/rebase/) |  |

## <a name="initOptions"></a><span>Rebase.</span>initOptions <span class="tags"><span class="sync">Sync</span><span class="experimental">Experimental</span></span>

```js
var result = Rebase.initOptions(opts, version);
```

| Parameters | Type |   |
| --- | --- | --- |
| opts | [RebaseOptions](/api/rebase_options/) | the `git_rebase_options` instance to initialize. |
| version | Number | the version of the struct; you should pass `GIT_REBASE_OPTIONS_VERSION` here. |

| Returns |  |
| --- | --- |
| Number |  Zero on success; -1 on failure. |

## <a name="open"></a><span>Rebase.</span>open <span class="tags"><span class="async">Async</span><span class="experimental">Experimental</span></span>

```js
Rebase.open(repo).then(function(rebase) {
  // Use rebase
});
```

| Parameters | Type |   |
| --- | --- | --- |
| repo | [Repository](/api/repository/) |  |

| Returns |  |
| --- | --- |
| [Rebase](/api/rebase/) |  |

## <a name="abort"></a><span>Rebase#</span>abort <span class="tags"><span class="sync">Sync</span><span class="experimental">Experimental</span></span>

```js
var result = rebase.abort(signature);
```

| Parameters | Type |
| --- | --- | --- |
| signature | [Signature](/api/signature/) | The identity that is aborting the rebase |

| Returns |  |
| --- | --- |
| Number |  Zero on success; GIT_ENOTFOUND if a rebase is not in progress,
         -1 on other errors. |

## <a name="commit"></a><span>Rebase#</span>commit <span class="tags"><span class="sync">Sync</span><span class="experimental">Experimental</span></span>

```js
var result = rebase.commit(id, author, committer, message_encoding, message);
```

| Parameters | Type |
| --- | --- | --- |
| id | [Oid](/api/oid/) | Pointer in which to store the OID of the newly created commit |
| author | [Signature](/api/signature/) | The author of the updated commit, or NULL to keep the author from the original commit |
| committer | [Signature](/api/signature/) | The committer of the rebase |
| message_encoding | String | The encoding for the message in the commit, represented with a standard encoding name. If message is NULL, this should also be NULL, and the encoding from the original commit will be maintained. If message is specified, this may be NULL to indicate that "UTF-8" is to be used. |
| message | String | The message for this commit, or NULL to use the message from the original commit. |

| Returns |  |
| --- | --- |
| Number |  Zero on success, GIT_EUNMERGED if there are unmerged changes in
        the index, GIT_EAPPLIED if the current commit has already
        been applied to the upstream and there is nothing to commit,
        -1 on failure. |

## <a name="finish"></a><span>Rebase#</span>finish <span class="tags"><span class="sync">Sync</span><span class="experimental">Experimental</span></span>

```js
var result = rebase.finish(signature, opts);
```

| Parameters | Type |
| --- | --- | --- |
| signature | [Signature](/api/signature/) | The identity that is finishing the rebase (optional) |
| opts | [RebaseOptions](/api/rebase_options/) | Options to specify how rebase is finished |

| Returns |  |
| --- | --- |
| Number |  |

## <a name="free"></a><span>Rebase#</span>free <span class="tags"><span class="sync">Sync</span><span class="experimental">Experimental</span></span>

```js
rebase.free();
```

## <a name="operationByIndex"></a><span>Rebase#</span>operationByIndex <span class="tags"><span class="sync">Sync</span><span class="experimental">Experimental</span></span>

```js
var rebaseOperation = rebase.operationByIndex(idx);
```

| Parameters | Type |
| --- | --- | --- |
| idx | Number | The index of the rebase operation to retrieve |

| Returns |  |
| --- | --- |
| [RebaseOperation](/api/rebase_operation/) |  The rebase operation or NULL if `idx` was out of bounds |

## <a name="operationCurrent"></a><span>Rebase#</span>operationCurrent <span class="tags"><span class="sync">Sync</span><span class="experimental">Experimental</span></span>

```js
var result = rebase.operationCurrent();
```

| Returns |  |
| --- | --- |
| Number |  The index of the rebase operation currently being applied. |

## <a name="operationEntrycount"></a><span>Rebase#</span>operationEntrycount <span class="tags"><span class="sync">Sync</span><span class="experimental">Experimental</span></span>

```js
var result = rebase.operationEntrycount();
```

| Returns |  |
| --- | --- |
| Number |  The number of rebase operations in total |
