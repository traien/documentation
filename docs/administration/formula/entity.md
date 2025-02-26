# Formula > Functions > Entity

Functions of the *Entity* group operate with a target record. There can be only one target record available in formula-script context.
For *Before Update Script*, the target record is the record that is currently updated. For Workflow's *Create Record* action,
the target record is the record is being created. For Workflow's conditions, the target record is the target record of the workflow rule.

* [entity\isNew](#entityisnew)
* [entity\isAttributeChanged](#entityisattributechanged)
* [entity\isAttributeNotChanged](#entityisattributenotchanged)
* [entity\attribute](#entityattribute)
* [entity\setAttribute](#entitysetattribute)
* [entity\attributeFetched](#entityattributefetched)
* [entity\addLinkMultipleId](#entityaddlinkmultipleid)
* [entity\hasLinkMultipleId](#entityhaslinkmultipleid)
* [entity\removeLinkMultipleId](#entityremovelinkmultipleid)
* [entity\isRelated](#entityisrelated)
* [entity\sumRelated](#entitysumrelated)
* [entity\countRelated](#entitycountrelated)
* [entity\getLinkColumn](#entitygetlinkcolumn)


## entity\isNew

`entity\isNew()`

Returns TRUE if the entity is new (being created) and FALSE if not (being updated).

## entity\isAttributeChanged

`entity\isAttributeChanged(ATTRIBUTE)`

Returns TRUE if ATTRIBUTE of the record was changed.

Example:

`entity\isAttributeChanged('status')`

## entity\isAttributeNotChanged

`entity\isAttributeNotChanged(ATTRIBUTE)`

Return TRUE if ATTRIBUTE of the record was not changed.

## entity\attribute

`entity\attribute(ATTRIBUTE)`

An ATTRIBUTE value of a target record. It's also possibe to fetch an attribute of a related record.

`$test = entity\attribute('name')` is equivalent to `$test = name`.

Examples:

`entity\attribute('assignedUserId')`

`entity\attribute('account.name')`

## entity\setAttribute

`entity\setAttribute(ATTRIBUTE, VALUE)`

Set ATTRIBUTE with a VALUE.

`entity\setAttribute('stage', 'Closed Won')` is equivalent to `stage = 'Closed Won'`.

Example:

`entity\setAttribute('stage', 'Closed Won')`


## entity\attributeFetched

`entity\attributeFetched(ATTRIBUTE)`

An ATTRIBUTE value that was set when a target record was fetched from database. Before it was modified.

Example:

`entity\attributeFetched('assignedUserId')`

Note: Should not be used in workflow and BPM actions, use `workflow\targetEntity\attributeFetched` instead.

## entity\addLinkMultipleId

`entity\addLinkMultipleId(LINK, ID)`

Adds ID to Link Multiple field.

`entity\addLinkMultipleId(LINK, ID_LIST)`

Adds the list of ids.

Example:

`entity\addLinkMultipleId('teams', 'someTeamId')`

Add 'someTeamId' to 'teams' field.


## entity\hasLinkMultipleId

`entity\hasLinkMultipleId(LINK, ID)`

Checks whether Link Multiple field has specific ID.

## entity\removeLinkMultipleId

`entity\removeLinkMultipleId(LINK, ID)`

Removes a specific ID from the Link Multiple field.

## entity\isRelated

`entity\isRelated(LINK, ID)`

Checks whether a target entity is related with another entity represented by LINK and ID.

## entity\sumRelated

`entity\sumRelated(LINK, FIELD, [FILTER])`

Sums related records by a specified FIELD with an optional FILTER.

Example:

`entity\sumRelated('opportunities', 'amountConverted', 'won')`

FILTER is a name of a filter pre-defined in the system. It's also possible to apply a [list report](../../user-guide/reports.md) as a filter. More [info](../formula.md#filter).

## entity\countRelated

`entity\countRelated(LINK, [FILTER])`

Returns a number of related records with an optional FILTER applied.

Example:

`entity\countRelated('opportunities', 'open')`

It's possible to apply a [list report](../../user-guide/reports.md) as a filter. More [info](../formula.md#filter).

## entity\getLinkColumn

`entity\getLinkColumn(LINK, ID, COLUMN)`

Fetches a relationship column value.

Example:

`entity\getLinkColumn('targetLists', 'TARGET_LIST_ID', 'optedOut')`
