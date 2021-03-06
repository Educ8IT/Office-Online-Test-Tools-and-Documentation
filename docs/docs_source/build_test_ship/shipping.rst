
..  _go live:
..  _shipping:

Shipping your Office Online integration
=======================================

..  spelling::

    rollout
    Rollout

Once you believe you are ready to ship your integration, you should contact Microsoft and explain that you believe
you are ready to ship. This will begin the 'go live' process, after which you will be able to ship your Office Online
integration.

The 'go live' process consists of three phases:

#. **Validation** - Microsoft will validate your WOPI implementation as well as your UI integration. Depending on what
   issues are uncovered during validation, this may take some time. You should estimate a two-week turnaround time
   assuming there are no major issues uncovered. However, we recommend allowing at least a month unless your
   integration is very simple.

   ..  tip::
       You can avoid delays in validation by ensuring that your implementation is consistent with this documentation
       and that the :ref:`validator` tests are passing.

#. **Production Smoke Test** - Microsoft will enable you to use the production Office Online environment for
   smoke-testing. This should be basic testing performed by the host since the production environment is slightly
   different than the test environment, and different issues may be uncovered. This can be as long or as short as the
   host deems necessary. Typically a week is enough time, though it can be much shorter.

#. **Sign off and roll out** - Once Microsoft has signed off on your integration, you can begin to roll out to your
   users. Depending on your traffic estimates, Microsoft may request that you roll out over a period of several days
   to ensure you do not overload Office Online or your WOPI servers.

You will need to provide some things to Microsoft as part of the 'go live' process. These are covered in detail in
the sections below.


Test accounts
-------------

In order to enable your WOPI host to use Office Online's :ref:`production environment <production environment>`,
Microsoft will perform some manual validation of your WOPI implementation and Office Online integration. This
requires that you provide Microsoft test accounts that they can use to test your integration. These test
accounts must be able to test your Office Online integration.

Once test accounts are provided, Microsoft will usually complete testing within two weeks. However, if issues are
uncovered testing may take longer.


Business user flow test accounts
--------------------------------

If you are using the :ref:`business user flow <Business editing>`, you will need test accounts from Microsoft in
order to effectively test the flow in the :ref:`dogfood`. See the :ref:`business user testing` section for more
information.


WOPI implementation questionnaire
---------------------------------

There are some aspects of your WOPI implementation that are particularly critical to the success of your integration.
In order to verify these parts of your implementation, Microsoft will ask you to answer some questions regarding
your specific WOPI implementation. These questions are included below.

..  note::
    This list of questions is subject to change. Microsoft will provide you with a specific list of questions as part
    of the 'go live' process that may differ from the list below.

#. Are all of the basic :ref:`validator` tests passing?

#. Please confirm that your File IDs meet the :term:`criteria listed in the documentation <file id>`. Office Online
   expects file IDs to be unique and consistent over time, as well as when accessed by different users or via
   different UI paths (e.g. a given file might be available in two different parts of your UI, such as in a typical
   folder and also in search results. If the document is meant to be the same, then the file IDs should match.
   Otherwise users will see unexpected behavior when they access the same file via different UI paths).

#. Please confirm you're providing a user ID using the :term:`UserId` field and that the ID is unique and consistent
   over time :ref:`as described here <User identity properties>`.

#. Please confirm that the value in the :term:`OwnerId` field represents the user who owns the document and is unique
   and consistent over time :ref:`as described here <User identity properties>`.

#. Are you setting any :ref:`User identity properties` other than :term:`UserId` and :term:`OwnerId`?

#. Are you sending the :term:`SHA256` value in :ref:`CheckFileInfo`? If not, please confirm that your version numbers
   change for each file version.

#. Under what conditions do you create new versions of files? Hosts often do this either when a file is unlocked or
   whenever a :ref:`PutFile` is received - either of these options is appropriate.

#. Are you using the :ref:`business user flow <Business editing>`?

#. What :ref:`supports properties` are you passing in :ref:`CheckFileInfo`?


Production settings check
-------------------------

Prior to enabling your integration in the :ref:`production environment <production environment>`, Microsoft will ask
you to verify your current :ref:`settings`, including your entries in the :ref:`allow list` and
:ref:`redirect domains`.

..  important::

    Remember that changes to production settings require time to make.

    ..  include:: /fragments/settings_change_warning.rst


Service management contacts
---------------------------

Office Online is a worldwide cloud service, and is thus monitored at all times. As part of the 'go live' process,
Microsoft will provide you with information regarding how to escalate service quality issues with Office Online's
on-call engineers.

In order to use the :ref:`production environment <production environment>`, you must also provide a contact for
Microsoft's on-call engineers to reach if Office Online detects an issue that we suspect is due to a problem on the
host side. For example, Office Online's monitoring systems might detect error rates for sessions spiking, and the
on-call engineer would contact the host to see if it's a known issue on the host side. Ideally this emergency contact
can be reached 24x7, either by phone or email.


Rollout schedule and traffic estimates
--------------------------------------

Typically Microsoft asks partners to roll out over a period of time - between a few days to two weeks - depending
on the anticipated traffic. For smaller hosts this is not always necessary. If you're already planning on doing this,
you should communicate the schedule to Microsoft (i.e. 10% day 1, 50% day 2, etc.). If you're not, you must
coordinate with Microsoft to ensure this is appropriate given your traffic estimates.

In order to best plan the rollout, you should be prepared to provide Microsoft with updated traffic estimates.
Ideally these will be broken down by view/edit, file type, and geography, but provide whatever you can.


Production access
-----------------

Once you and Microsoft have agreed on a rollout plan and Microsoft has signed off on your WOPI implementation, your
WOPI host will be enabled in the :ref:`production environment <production environment>`. You should plan to do some
basic testing against the production environment prior to rollout to ensure there are no unique issues using that
environment. Once you have completed that testing, you can roll your integration out to users according the
agreed-upon rollout schedule.
