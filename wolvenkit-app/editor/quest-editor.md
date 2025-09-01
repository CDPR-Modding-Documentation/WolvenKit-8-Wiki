---
description: Quest Editor 101
---

# Quest Editor

The Quest Editor is designed to work .questphase files. It enables a node-based workflow: you select a node on the graph editor to edit and inspect its properties.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Wolvenkit's Quest Editor</p></figcaption></figure>

{% hint style="danger" %}
Undo and redo actions are currently **not supported** but are planned.&#x20;

Be careful with your edits and it wouldn't hurt to make periodical backups anyways!
{% endhint %}

## **Right-click context menu**

**Common actions:**

* Duplicate Node: Creates an exact copy of the selected node, including all its properties, but with a new unique ID and no connections.
* Detach Node: Removes all incoming and outgoing connections from the selected node.
* Delete Node (Soft Delete): Replaces the selected node with a special '[Deletion Marker](https://nativedb.red4ext.com/c/5548111434222821)' node.  This is the default deletion for any signal-stopping node such as a PauseCondition, Choice, etc. This is the recommended way to remove such nodes from quests that have already been published, as it prevents users with existing saves from getting stuck in a signal-stopping node.&#x20;
* Destroy Node (Hard Delete): Permanently removes the selected node from the graph. This is safe to use when creating a new scene, but should be used with caution on signal-stopping scene nodes that are already in use, as it can cause user to be stuck in your quest.
* Convert to Phase: Converts the selected nodes and packages them into a Phase node. Does not alter any logic and preserves all incoming and outgoing sockets.&#x20;



**Unique actions:**

* Recalculate Sockets for Phase and Scene nodes: syncs new in/out sockets created inside a Phase or Scene.
* Add Output for Randomizer node: creates a new output node on the Randomizer node
* Add Case for Switch node: creates a new switch case output + condition pair\


## Shortcuts

| Shortcut                                                     | Action                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Delete`                                                     | <p>Performs a "soft delete" by replacing the node with a 'Deletion Marker' (soft delete). This only happens if the editor finds the selected node is a signal-stopping node like a Pause Condition, Choice, etc.</p><p>If it's a regular (non signal-stopping) node, it will be permanently deleted. </p><p>If it's already a 'Deletion Marker', it gets permanently destroyed. </p> |
| `Shift` + `Delete`                                           | Permanently destroys the selected node(s) (hard delete).                                                                                                                                                                                                                                                                                                                             |
| `Ctrl` + `D`                                                 | Duplicates the currently selected node.                                                                                                                                                                                                                                                                                                                                              |
| `Ctrl` + `N`                                                 | Opens the dialog to create a new node.                                                                                                                                                                                                                                                                                                                                               |
| `Ctrl` + `G`                                                 | Opens the "Go to Node" dialog to jump to a specific node by its ID.                                                                                                                                                                                                                                                                                                                  |
| `↑` `↓` `←` `→` (Arrow Keys)                                 | Navigates between nodes. The editor uses a "smart walk" system that considers both spatial position and connection history to determine the next node to select.                                                                                                                                                                                                                     |
| `Alt` + `Click` on a socket or `Right-click` on a connection | Deletes connection                                                                                                                                                                                                                                                                                                                                                                   |

