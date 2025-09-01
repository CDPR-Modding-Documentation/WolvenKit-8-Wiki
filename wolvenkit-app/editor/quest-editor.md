---
description: Quest Editor 101
---

# Quest Editor

The Quest Editor is designed to work .questphase files. It enables a node-based workflow: you select a node on the graph editor to edit and inspect its properties.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Wolvenkit's Quest Editor</p></figcaption></figure>

## **Right-click context menu**

**Common actions:**

* Duplicate Node: Creates an exact copy of the selected node, including all its properties, but with a new unique ID and no connections.
* Detach Node: Removes all incoming and outgoing connections from the selected node.
* Delete Node (Soft Delete): Replaces the selected node with a special '[Deletion Marker](https://nativedb.red4ext.com/c/5548111434222821)' node. This is the recommended way to remove nodes from quests that have already been published, as it prevents users with existing saves from getting stuck.
* Destroy Node (Hard Delete): Permanently removes the selected node from the graph. This is safe to use when creating a new scene, but should be used with caution on scenes that are already in use, as it can corrupt user saves.i
* Recalculate Sockets: Performed on Phase and Scene nodes. Use this to sync new in/out sockets created inside a Phase or Scene.
* Convert to Phase: Converts the selected nodes and packages them into a Phase node. Does not alter any logic and preserves all incoming and outgoing sockets.&#x20;

{% hint style="danger" %}
Undo and redo actions are currently **not supported** but are planned.&#x20;

Be careful with your edits and it wouldn't hurt to make periodical backups anyways!
{% endhint %}

## Shortcuts

| Shortcut                                                     | Action                                                                                                                                                                                                                              |
| ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Delete`                                                     | Performs a "soft delete". If the selected node is a regular node, it's replaced with a 'Deletion Marker' (soft delete). If it's already a 'Deletion Marker', it gets permanently destroyed. This does not apply to Start/End nodes. |
| `Shift` + `Delete`                                           | Permanently destroys the selected node(s) (hard delete).                                                                                                                                                                            |
| `Ctrl` + `D`                                                 | Duplicates the currently selected node.                                                                                                                                                                                             |
| `Ctrl` + `N`                                                 | Opens the dialog to create a new node.                                                                                                                                                                                              |
| `Ctrl` + `G`                                                 | Opens the "Go to Node" dialog to jump to a specific node by its ID.                                                                                                                                                                 |
| `↑` `↓` `←` `→` (Arrow Keys)                                 | Navigates between nodes. The editor uses a "smart walk" system that considers both spatial position and connection history to determine the next node to select.                                                                    |
| `Alt` + `Click` on a socket or `Right-click` on a connection | Deletes connection                                                                                                                                                                                                                  |

